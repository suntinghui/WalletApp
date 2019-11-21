<template>
	<view>
		<view class="bg-white padding text-center">
			<image src="../../../static/img-tiaoxingma.png" mode="widthFix" style="width: 100%;"></image>
			<view class=" text-gray">2000 <text>****</text> 查看数字</view>
			<image src="../../../static/img-erweima.png" mode="widthFix" style="width: 60%;" class="margin-top-lg"></image>
		</view>
		<view class="cu-list menu bg-white select-payment solid-top">
			<view class="cu-item arrow border-top">
				<button class="cu-btn content" @tap="showModal" data-target="bottomModal">
					<image src="../../../static/icon-huabei.png" class="png" mode="aspectFit"></image>
					<view class="text-grey text-left">
						<view class="font-bold">花呗分期</view>
						<view>优先使用此付款方式</view>
					</view>
				</button>
			</view>
		</view>
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
	.select-payment{
	 padding: 10px 0;
	}

</style>
