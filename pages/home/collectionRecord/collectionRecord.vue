<template>
	<view>
		<view class="cu-bar bg-white solid-bottom">
			<view class="action">
				<text class="cuIcon-title text-orange"></text> <text class="text-bold">2019-11-10</text>
			</view>
			<view class="action">
				<button class="cu-btn bg-white" @tap="showModal" data-target="menuModal"><text class="cuIcon-calendar"></text>自定义查询</button>
			</view>
		</view>
		<view class="cu-list menu sm-border">
			<view class="cu-item">
				<view class="content">
					<text class="text-grey">收款笔数1</text>
				</view>
				<view class="action">
					<text class="text-grey text-sm">收款共计1992</text>
				</view>
			</view>
			<view class="cu-item">
				<view class="content padding-tb-sm">
					<view>
						<text class="text-blue margin-right-xs"></text> *国花</view>
					<view class="text-gray">
						<text class="margin-right-xs"></text> 15:12:11</view>
				</view>
				<view class="action">
					<text class="text-xxl text-danger">+1992</text>
				</view>
			</view>
			<view class="cu-item">
				<view class="content padding-tb-sm">
					<view>
						<text class="text-blue margin-right-xs"></text> *国花</view>
					<view class="text-gray">
						<text class="margin-right-xs"></text> 15:12:11</view>
				</view>
				<view class="action">
					<text class="text-xxl text-green">-100</text>
				</view>
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
