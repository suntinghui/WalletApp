<template>
	<view>
		<view class="bg-title text-white text-center padding-lg">
			<view>
				通用额度可用(元)
			</view>
			<view class="amount">
				40893.00
			</view>
			<view>
				这月买  下月还  0费用
			</view>
			<view class="m-t-10">
				<button class="cu-btn round bg-white" @click="showDetail">查看详情</button>
			</view>
		</view>
		<view class="cu-list grid col-2 no-border card-menu margin-top">
			<view class="cu-item">
				<navigator url="../../huabei/byBill/byBill" hover-class="none">
					<view class="tui-grid-label">我的账单</view>
					<view class="text-sm text-gray" style="height: 40rpx;">还款日本月10号</view>
					<view class=" text-gray"></view>
				</navigator>
			</view>
			<view class="cu-item">
				<view @click="showDetail">
					<view class="tui-grid-label">钱包花呗</view>
					<view class="text-sm text-gray" style="height: 40rpx;">通用额度</view>
					<view class="text-danger font-bold">฿495034.00</view>
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

export default {
	components: {

	},
	data() {
		return {

		};
	},

	methods: {
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
		}
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
