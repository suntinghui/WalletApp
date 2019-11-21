<template>
	<view>
		<swiper class="swiper" :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval" :duration="duration">
			<swiper-item>
				<image src="../../../static/slider-01.png" class="slider-item" mode="widthFix"></image>
			</swiper-item>
			<swiper-item>
				<image src="../../../static/slider-01.png" class="slider-item" mode="widthFix"></image>
			</swiper-item>
			<swiper-item>
				<image src="../../../static/slider-01.png" class="slider-item" mode="widthFix"></image>
			</swiper-item>
		</swiper>
		<view class="cu-list grid col-3 no-border text-grid card-menu shadow shadow-lg" style="margin-top: -20px; position: relative; z-index: 9999;">
			<view class="cu-item" @click="scan">
				<view class="iconfont cu-grid-icon">&#xe629;</view>
				<text class="text-grid">扫一扫</text>
			</view>
			<view class="cu-item">
				<navigator url="../../home/payment/payment" hover-class="none">
					<view class="iconfont cu-grid-icon">&#xe639;</view>
					<text class="text-grid">付款</text>
				</navigator>
			</view>
			<view class="cu-item">
				<navigator url="../../home/receipt/receipt"  hover-class="none">
					<view class="iconfont cu-grid-icon">&#xe628;</view>
					<text class="text-grid">收款</text>
				</navigator>
			</view>
		</view>

		<view class="cu-list grid col-2 no-border card-menu shadow shadow-lg">
			<view class="cu-item solid-right">
				<navigator url="../../home/withdraw/withdraw" hover-class="none">
					<view class="">余额</view>
					<view class="text-sm text-gray" style="height: 40rpx;"></view>
					<view class="text-danger font-bold">฿100.00</view>
				</navigator>
			</view>
			<view class="cu-item" @tap="showHuabei" >
				<view>
					<view class="">钱包花呗</view>
					<view class="text-sm text-gray" style="height: 40rpx;">通用额度</view>
					<view class="text-danger font-bold">฿495034.00</view>
				</view>
			</view>
		</view>

		<view class="cu-list menu sm-border card-menu shadow shadow-lg">
			<view class="cu-item arrow">
				<navigator url="../../home/billLists/billLists" hover-class="none" class="content">
					<image src="/static/icon-zhangdan.png" class="png" mode="aspectFit"></image>
					<text class="text-grey">账单</text>
				</navigator>
			</view>
			<view class="cu-item arrow">
				<navigator url="../../home/merchantService/merchantService" hover-class="none" class="content">
					<image src="/static/icon-shangjia.png" class="png" mode="aspectFit"></image>
					<text class="text-grey">商家服务</text>
				</navigator>
			</view>
			<navigator url="../../home/bankCard/bankCard" hover-class="none" class="cu-item arrow">
				<view class="content">
					<image src="/static/icon-yinhangka.png" class="png" mode="aspectFit"></image>
					<text class="text-grey">银行卡</text>
				</view>
			</navigator>
		</view>

	</view>
</template>
<script>
	export default {
		components: {

		},
		data() {
			return {
				indicatorDots: true,
				autoplay: true,
				interval: 2000,
				duration: 500
			};
		},

		methods: {
			scan: function() {
				uni.scanCode({
					success: (res) => {
						uni.showModal({
							title:'扫码成功',
							content:res.result,
							confirmText:'确定',
							showCancel:false
						})
					}
				});
			},
			changeIndicatorDots(e) {
				this.indicatorDots = !this.indicatorDots;
			},
			changeAutoplay(e) {
				this.autoplay = !this.autoplay;
			},
			intervalChange(e) {
				this.interval = e.target.value;
			},
			durationChange(e) {
				this.duration = e.target.value;
			},
			showHuabei: function(e) {
				uni.switchTab({
					url: '../huabei/huabei'
				})
			}
		}
	};
</script>

<style lang="scss">
	.cu-grid-icon {
		font-size: 70upx;
	}

	.slider-item {
		width: 100%;
	}

	.tui-list-cell-name {
		padding-left: 5px;
	}

	.text-grid {
		color: $uni-color-primary !important;
	}
</style>
