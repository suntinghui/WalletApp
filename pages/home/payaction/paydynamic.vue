<template>
	<view>
		<view class="padding bg-white">
			
			<view class="text-black">金额</view>
			
			<view class="flex margin solid-bottom">
				<view class="text-price text-sl"></view>
				<input type="digit" v-model="amount" :disabled="changeAmount" style="min-height:50px; height: 50px;" class="text-bold text-sl padding-lr-lg" />
			</view>
			
			<view class="padding flex flex-direction">
					<button class="cu-btn bg-green margin-tb-sm lg radius" @tap="doPay()">确定</button>
			</view>
			
		</view>
		
	</view>

</template>

<script>
	
	import {
		mapMutations,
		mapGetters
	} from 'vuex';
	
	var _this;
	
	export default {
		data() {
			return {
				// 	// {"codeType":"0","spAccountType":["10","30"],"customerNbr":"201912111358253623e514d31","userPhoto":"","customerName":"2","merchantName":"2",
				// "merchantNbr":"201912111358253623e514d31","payerAccountNbr":"","transferAmount":1209,"orderNbr":"","transferDesc":"","transferStatus":"",
				// "hasTransferAmount":true,"creditFree":false,"hbFree":false,"hbfqFree":false,"maxFreeMonth":0,"minFreeAmount":0,
				// "creditInterestRate":0,"hbInterestRate":0.01,"hbfqMinAmount":100,"hbfqInterestRate":{"3":0.01,"6":0.01,"12":0.01,"360":0.005},"signStatus":"true"}
				transferInfo: {},
				amount: "",
				scancode:"",
				
				intervalPayID: 0,
			}
		},
		
		computed: {
			...mapGetters(["token", "userInfo"]),
		},
		
		onLoad(options) {
			console.log(options.data)
			this.transferInfo = JSON.parse(options.data);
			this.scancode = options.scancode;
		},
		
		onShow: function() {
			_this = this;
		},
		
		onUnload() {
			this.stopRefreshPayStatusTask();
		},

		methods: {
			...mapMutations(['updateToken', "setUserInfo"]),
			
			doPay() {
				if(this.amount == '' || Number(this.amount) == 0) {
					this.$api.msg("请输入付款金额")
				} else {
					// 等待用户操作
				}
			},
			
			
			// 动态收款处理
			transferDynamicPay() {
				uni.request({
					url: this.BASE_URL + '/transfer/scan/code/dynamic/pay',
					method: 'POST',
					header: {
						'Content-Type': 'application/x-www-form-urlencoded',
						'token': _this.token
					},
					data: {
						code: _this.scancode,
						transferAmount:_this.amount,
						orderNbr: new Date().getTime()
					},
					success: (res) => {
						console.log(JSON.stringify(res));
						if (res.data.code == "B0000") {
							
							_this.$token.updateToken(res.header.token);
							
							uni.navigateTo({
								url:'/pages/home/transferSuccess/transferSuccess'
							})
							
						} else {
							
							 _this.startRefreshPayStatusTask()
							
							_this.$api.loading(res.data.msg)
						}
					},
					fail: (res) => {},
					complete: (res) => {
						uni.hideLoading();
					}
				});
			},
			
			startRefreshPayStatusTask() {
				this.intervalPayID = setInterval(this.refreshPayStatus, 2 * 1000);
			},
			
			stopRefreshPayStatusTask() {
				console.log("停止定时刷新。。。")
				clearInterval(this.intervalPayID);
			},
			
			refreshPayStatus: function() {
				uni.request({
					url: this.BASE_URL + '/transfer/scan/pay/status',
					method: 'POST',
					header: {
						'Content-Type': 'application/x-www-form-urlencoded',
						'token': _this.token
					},
					data: {
						code: _this.val
					},
					success: (res) => {
						console.log(JSON.stringify(res));
			
						if (res.data.code == "B0000") {
							if (res.data.data.status == '6') {
								uni.navigateTo({
									url:'/pages/home/transferSuccess/transferSuccess'
								})
							}
			
						}
						_this.$token.updateToken(res.header.token);
			
					},
					fail: (res) => {},
					complete: (res) => {
						uni.hideLoading();
					}
				});
			},
			
		},
		
	}
</script>

<style>
	/* 提示窗口 */
	
	.pay-modal {
		width: 550upx;
		background: #fff;
	}
	
	
	.pay-modal-pwd {
		width: 100%;
		margin-top: 15px;
	}

</style>
