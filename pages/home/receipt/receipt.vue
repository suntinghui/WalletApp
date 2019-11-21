<template>
	<view>
		<view class="bg-white text-center padding-lg">
			<image src="../../../static/img-erweima.png" mode="widthFix" style="width: 60%;" class="margin-top-lg"></image>
			<view class="flex margin-top-lg  text-blue">
				<navigator url="../setAmount/setAmount"  hover-class="none" class="flex-sub solid-right">
					设置金额
				</navigator>
				<view class="flex-sub">
					保存图片
				</view>
			</view>
		</view>
		<view class="cu-list menu sm-border margin-top">
			<view class="cu-item arrow">
				<navigator class="content" hover-class="none" url="../collectionRecord/collectionRecord">
					<text class="cuIcon-text text-grey"></text>
					<text class="text-grey">收款纪录</text>
				</navigator>
			</view>
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

</style>
