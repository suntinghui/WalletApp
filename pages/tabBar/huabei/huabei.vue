<template>
	<view>
		<view class="bg-title text-white text-center padding-lg">
			<view>
				通用额度可用(元)
			</view>
			<view class="amount">
				{{this.userInfo.creditAmount}}
			</view>
			<view>
				这月买  下月还  {{this.userInfo.nextMonthRepaymentBalance}}费用
			</view>
			<view class="m-t-10">
				<button class="cu-btn round bg-white" @click="showDetail">查看详情</button>
			</view>
		</view>
		<view class="cu-list grid col-2 no-border card-menu margin-top">
			<view class="cu-item">
				<navigator url="../../huabei/byBill/byBill" hover-class="none">
					<view class="tui-grid-label">我的账单</view>
					<view class="text-sm text-gray" style="height: 40rpx;">还款日本月{{this.userInfo.repaymentDate}}号</view>
					<view class=" text-gray"></view>
				</navigator>
			</view>
			<view class="cu-item">
				<view @click="showDetail">
					<view class="tui-grid-label">钱包花呗</view>
					<view class="text-sm text-gray" style="height: 40rpx;">通用额度</view>
					<view class="text-danger font-bold">฿ {{this.userInfo.creditAmount}}</view>
				</view>
			</view>
		</view>
		<view class="cu-list menu sm-border card-menu">
			<view class="cu-item arrow" @tap="showRepayment">
				<view class="content">
					<image src="/static/icon-lijihuankuan.png" class="png" mode="aspectFit"></image>
					<text class="text-grey">立即还款</text>
				</view>
			</view>
			<view class="cu-item arrow" @tap="showStaging">
				<view class="content">
					<image src="/static/icon-zhangdanfenqi.png" class="png" mode="aspectFit"></image>
					<text class="text-grey">账单分期</text>
				</view>
			</view>
			<view class="cu-item arrow" @tap="showPaymentCode">
				<view class="content">
					<image src="/static/icon-fenqima.png" class="png" mode="aspectFit"></image>
					<text class="text-grey">分期码</text>
				</view>
			</view>
		</view>
		
	</view>
</template>
<script>
	
	var _this;
	
	import {
		mapMutations, mapGetters
	} from 'vuex';

export default {
	data() {
		return {

		};
	},
	
	onLoad:function(){
		_this = this;
	},
	
	onShow:function(){
		this.getUserInfo();
	},
	
	computed: {
		...mapGetters(["token", "userInfo"]),
	},

	methods: {
		...mapMutations(['updateToken', 'logout', "setUserInfo"]),
		
		showRepayment: function(e) {
			uni.navigateTo({
				url: "../../huabei/repayment/repayment"
			})
		},
		showStaging: function(e) {
			uni.navigateTo({
				url: "../../huabei/staging/staging"
			})
		},
		showDetail: function(e) {
			uni.navigateTo({
				url: "../../huabei/quota/quota"
			})
		},
		showPaymentCode: function(e) {
			uni.navigateTo({
				url: "../../huabei/payment-code/payment-code"
			})
		},
		
		getUserInfo: function(e) {
			
			uni.request({
			    url: this.BASE_URL+'/login/query/userInfo',
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
						_this.setUserInfo(res.data.data);
						
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
};
</script>

<style lang="scss">
.amount{
	font-size: 60upx;
	font-weight: bold;
	padding: 10px 0;
}
.bg-title{
	background: $uni-color-primary;
}
</style>
