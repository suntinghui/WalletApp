<template>
	<view>
		<view class="cu-list grid col-1 no-border card-menu shadow shadow-lg">
			<view class="text-center padding-sm">
				<view class="text-gray">余额</view>
				<view class="text-danger font-bold text-price text-xxl">{{merchantInfo.history.balance}}</view>
			</view>
		</view>

		<view class="cu-list grid col-2 no-border card-menu shadow shadow-lg">
			<view class="text-center padding-sm solid-bottom">
				<view class="text-black">总收入：{{merchantInfo.history.sumIn}}元</view>
			</view>

			<view class="text-center padding-sm solid-bottom">
				<view class="text-black">退款：{{merchantInfo.history.sumBack}}元</view>
			</view>

			<view class="text-center padding-sm">
				<view class="text-black">钱包：{{merchantInfo.history.amountQb}}元</view>
				<view class="text-black margin-top">银行卡：{{merchantInfo.history.amountCard}}元</view>
			</view>

			<view class="text-center padding-sm">
				<view class="text-black">花呗：{{merchantInfo.history.amountHb}}元</view>
				<view class="text-black margin-top">花呗分期：{{merchantInfo.history.amountHbfq}}元</view>
			</view>

		</view>
		
		
		<view class="cu-list grid col-2 no-border card-menu shadow shadow-lg">
			<view class="text-center padding-sm solid-bottom">
				<view class="text-black">收入：{{merchantInfo.today.sumIn}}元</view>
			</view>
		
			<view class="text-center padding-sm solid-bottom">
				<view class="text-black">退款：{{merchantInfo.today.sumBack}}元</view>
			</view>
		
			<view class="text-center padding-sm">
				<view class="text-black">钱包：{{merchantInfo.today.amountQb}}元</view>
				<view class="text-black margin-top">银行卡：{{merchantInfo.today.amountCard}}元</view>
			</view>
		
			<view class="text-center padding-sm">
				<view class="text-black">花呗：{{merchantInfo.today.amountHb}}元</view>
				<view class="text-black margin-top">花呗分期：{{merchantInfo.today.amountHbfq}}元</view>
			</view>
		
		</view>



	</view>
</template>

<script>
	var _this;
	
	import permision from "@/common/permission.js"
	
	import {
		mapMutations, mapGetters
	} from 'vuex';
	
	export default {
		data() {
			return {
				merchantInfo: null
			}
		},
		
		onLoad:function(){
			_this = this;
		},
		
		onShow() {
			this.queryInfo();
		},
		
		computed: {
			...mapGetters(["token", "userInfo"]),
		},
		
		methods: {
			...mapMutations(['updateToken', "setUserInfo"]),
			
			queryInfo:function() {
				this.$api.loading("正在加载")
				
				uni.request({
				    url: this.BASE_URL+'/merchant/query/merchantAmount',
					method: 'POST',
					header: {
						'Content-Type': 'application/x-www-form-urlencoded',
						'token': _this.token
					},
				    data: {
				    },
				    success: (res) => {
						console.log(JSON.stringify(res));
						if (res.data.code == "B0000") {
							_this.merchantInfo = res.data.data
							
							_this.$token.updateToken(res.header.token);
							
						} else {
							console.log(res.data.msg)
						}
				    },
					fail: (res) => {
					},
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
