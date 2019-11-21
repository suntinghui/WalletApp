<template>
	<view class="cu-list menu sm-border">
		<view class="cu-item arrow">
			<view class="content margin" @click="showDetail">
				<text class="text-black text-bold">通用额度 · 可用</text>
				<view class="text-blue text-bold amount" >{{useableAmount}}</view>
				<view class="bottomAmount">
					<view class="amountInfo">
						<text class="text-df text-black text-bold">{{totalAmount}}</text>
						<text class="text-sm text-gray">总额度</text>
					</view>
					
					<view class="vline">
					</view>
					
					<view class="amountInfo">
						<text class="text-df text-black text-bold">{{surplusAmount}}</text>
						<text class="text-sm text-gray">已用额度</text>
					</view>
					
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import util from '@/common/util.js'
	
	export default {
		data() {
			return {
				totalAmount: util.formatAmount(41000, 2),
				useableAmount: util.formatAmount(40893, 2),
				surplusAmount: util.formatAmount(107, 2)
			}
		},
		methods: {
			showDetail: function(e) {
				uni.navigateTo({
					url: "../quota-detail/quota-detail"
				})
			}
		}
	}
</script>

<style>
	.amount {
		font-size: 60upx;
		margin-top: 20upx;
		margin-bottom: 20upx;
	}
	
	.bottomAmount {
		display: flex;
		flex-direction: row;
		margin-top: 40upx;
		align-items: center;
	}
	
	.amountInfo {
		display: flex;
		flex-direction: column;
	}
	
	.vline {
		margin-left: 30upx;
		margin-right: 30upx;
		height: 70upx;
		width: 1px;
		background-color: #CCCCCC;
	}

</style>
