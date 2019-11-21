<template>
	<view>
		<view class="cu-list menu border">
			<view class="cu-item">
				<view class="content">
					<text class="text-grey">请绑定持卡人本人的银行卡</text>
				</view>
			</view>
		</view>
		<form>
			<view class="cu-form-group solid-top">
				<view class="title">持卡人</view>
				<input value="王志亮" name="input" disabled=""></input>
				<text class='cuIcon-info text-orange'></text>
			</view>
			<view class="cu-form-group">
				<view class="title">卡号</view>
				<input placeholder="请输入卡号" name="input"></input>
				<text class='cuIcon-camera text-orange'></text>
			</view>
		</form>
		<view class="padding flex flex-direction">
				<navigator class="cu-btn bg-red margin-tb-sm lg radius" url="../../home/addBankCard-02/addBankCard-02">下一步</navigator>
			
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			
		}
	}
</script>

<style>
.cu-form-group .title {
		min-width: calc(4em + 15px);
	}
</style>
