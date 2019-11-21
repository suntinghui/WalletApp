<template>
	<view>
		<view class="cu-list menu border">
			<view class="cu-item">
				<view class="content">
					<text class="text-grey">请选择银行卡类型</text>
				</view>
			</view>
		</view>
		<form>
			<view class="cu-form-group solid-top">
				<view class="title">银行</view>
				<picker @change="PickerChange" :value="index" :range="bankLists">
					<view class="picker" style="text-align: left;">
						{{index>-1?bankLists[index]:'请选择银行卡'}}
					</view>
				</picker>
			</view>
			<view class="cu-form-group">
				<view class="title">卡类型</view>
				<picker @change="PickerChange" :value="index" :range="bankType">
					<view class="picker" style="text-align: left;">
						{{index>-1?bankType[index]:'请选择银行卡类型'}}
					</view>
				</picker>
			</view>
			<view class="cu-form-group">
				<view class="title">手机号</view>
				<input placeholder="请输入银行预留的手机号" name="input"></input>
				<text class='cuIcon-info text-orange'></text>
			</view>
		</form>
		<view class="padding flex flex-direction">
			<navigator class="cu-btn bg-red margin-tb-sm lg radius" url="../../home/addBankCard-03/addBankCard-03">下一步</navigator>

		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				index: -1,
				bankLists: ['中国银行', '建设银行', '工商银行'],
				bankType: ['信用卡', '储蓄卡'],
			}
		},
		methods: {
			PickerChange(e) {
				this.index = e.detail.value
			},
		}
	}
</script>

<style>
	.cu-form-group .title {
		min-width: calc(4em + 15px);
	}
</style>
