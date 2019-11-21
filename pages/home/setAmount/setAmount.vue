<template>
	<view>
		<form>
			<view class="cu-form-group">
				<view class="title">金额</view>
				<input placeholder="请输入金额" name="input"></input>
			</view>
			<view class="cu-form-group align-start">
				<view class="title">理由</view>
				<textarea maxlength="-1" :disabled="modalName!=null" @input="textareaBInput" placeholder="请输入理由"></textarea>
			</view>
			<view class="padding flex flex-direction">
				<button class="cu-btn bg-orange margin-tb-sm lg">确定</button>
			</view>
		</form>
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

</style>
