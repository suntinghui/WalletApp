<template>
	<view>
		<view class="bg-white padding">
			<view class="flex">
				<view class="flex-sub">到账银行卡</view>
				<view class="flex-twice">
					<view class="cu-list menu no-border" style="padding: 0;">
						<view class="cu-item arrow" @tap="showModal" data-target="bottomModal">
							<view class="content">
								<view>
									<text class="cuIcon-clothesfill text-blue margin-right-xs"></text> 中国工商银行</view>
								<view class="text-gray text-sm">
									<text class="margin-right-xs"></text> 2小时内到账</view>
							</view>
						</view>
					</view>
				</view>
			</view>
			<view class="flex">
				<view class="flex-sub padding-tb-sm">提现金额</view>

			</view>
			<view class="cu-form-group solid-bottom">
				<view class="title text-bold text-right" style="font-size: 50rpx;">￥</view>
				<input placeholder="输入金额" name="input" class="text-bold" style="font-size: 55rpx; height: 60px; line-height: 60px;"></input>
			</view>
			<view class="padding-tb text-sm">
				零钱余额￥2806，<text class="text-blue">全部提现</text>
			</view>

			<!--选择银行-->
			<view class="cu-modal bottom-modal" :class="modalName=='bottomModal'?'show':''">
				<view class="cu-dialog">
					<view class="cu-bar bg-white">
						<view class="action text-green">确定</view>
						<view class="action text-blue" @tap="hideModal">取消</view>
					</view>
					<view class="">
						<radio-group class="block" @change="RadioChange">
							<view class="cu-form-group">
								<view class="title">花呗</view>
								<radio :class="radio=='A'?'checked':''" :checked="radio=='A'?true:false" value="A"></radio>
							</view>
							<view class="cu-form-group">
								<view class="title">工商银行</view>
								<radio :class="radio=='B'?'checked':''" :checked="radio=='B'?true:false" value="B"></radio>
							</view>
							<view class="cu-form-group">
								<view class="title">农业银行</view>
								<radio :class="radio=='C'?'checked':''" :checked="radio=='C'?true:false" value="C"></radio>
							</view>
							<view class="cu-form-group">
								<view class="title">建设银行</view>
								<radio :class="radio=='D'?'checked':''" :checked="radio=='D'?true:false" value="D"></radio>
							</view>
						</radio-group>
					</view>
				</view>
			</view>
			<!--选择银行-->

		</view>
		<view class="padding flex flex-direction">
			<button class="cu-btn bg-red margin-tb-sm lg" >提现</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				modalName: null,
				radio: 'A',
			}
		},
		methods: {
			showModal(e) {
				this.modalName = e.currentTarget.dataset.target
			},
			hideModal(e) {
				this.modalName = null
			},
			RadioChange(e) {
				this.radio = e.detail.value
			},
		}
	}
</script>

<style>

</style>
