<template>
	<view>
		<view class="cu-list menu sm-border">
			<view class="cu-item">
				<view class="content padding-tb-sm">
					<view class="text-gray">本月</view>
					<view class="text-black">支出 ¥ {{sumPay}}  收入 ¥ {{sumIncome}} </view>
				</view>
			</view>
		</view>
		<view class="cu-list menu-avatar">
			<view class="cu-item" v-for="(item, index) in dataList">
				
				<view class="cu-avatar lg" style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big10001.jpg);"></view>
				<view class="content">
					<view class="text-cut">{{item.transferDesc}}</view>
					<view class="text-gray text-sm flex">
						<view class="text-cut">{{item.transferDatetime}}</view>
					</view>
				</view>
				<view class="action">
					<!--  0=支出  1=收入 -->
					<view class="text-bold text-price text-red" v-if="item.transferDirection == 0">-{{item.transferAmount}}</view>
					<view class="text-bold text-price text-green" v-if="item.transferDirection == 1">{{item.transferAmount}}</view>
					<view class="cu-tag round bg-grey">{{item.transferType}}</view>
				</view>
			</view>
			
		</view>
	</view>
</template>

<script>
	var _this;
	
	import permision from "@/common/permission.js"
	
	import {
		mapMutations,
		mapGetters
	} from 'vuex';
	
	export default {
		data() {
			return {
				dataList:[],
				sumIncome: 0.00,
				sumPay: 0.00,
			}
		},
		
		onLoad: function() {
			_this = this;
		
			this.getHistoryList();
		},
		
		computed: {
			...mapGetters(["token", "userInfo"]),
		},
		
		methods: {
			...mapMutations(['updateToken', "setUserInfo"]),

			getHistoryList:function() {
				uni.request({
					url: this.BASE_URL + '/transfer/query/transferInfo/currentMonth',
					method: 'POST',
					header: {
						'Content-Type': 'application/x-www-form-urlencoded',
						'token': _this.token
					},
					data: {
						accountType: '10,205,206,301,311,30,31,399',
						queryType: '0'
					},
					success: (res) => {
						console.log(JSON.stringify(res));
						if (res.data.code == "B0000") {
							
							_this.dataList = res.data.data.detail;
							_this.sumPay = res.data.data.sumPay;
							_this.sumIncome = res.data.data.sumIncome;
							
							_this.$token.updateToken(res.header.token);
							
						} else {
							_this.$api.alert(res.data.msg)
						}
					},
					fail: (res) => {},
					complete: (res) => {
						uni.hideLoading();
					}
				});
			},
			
		}
	}
</script>

<style>

</style>
