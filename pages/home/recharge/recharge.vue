<template>
	<view>
		<view class="bg-white padding">
			<view class="flex">
				<view class="flex-sub">充值方式</view>
				<view class="flex-twice">
					<view class="cu-list menu no-border" style="padding: 0;">
						<view class="cu-item arrow" @tap="showModal" data-target="bottomModal">
							<view class="content">
								<view>
									<text class="cuIcon-clothesfill text-blue margin-right-xs"></text> 中国工商银行
								</view>
								<view class="text-gray text-sm">
									<text class="margin-right-xs"></text> 单日交易限额￥5000.00元
								</view>
							</view>
						</view>
					</view>
				</view>
			</view>
			
			<view class="flex">
				<view class="flex-sub padding-tb-sm">充值金额</view>
			</view>
			
			<view class="cu-form-group solid-bottom">
				<view class="title text-bold text-right" style="font-size: 50rpx;">￥</view>
				<input placeholder="" name="input" type="digit" class="text-bold" style="font-size: 55rpx; height: 60px; line-height: 60px;"></input>
			</view>

			<!--选择银行-->
			<view class="cu-modal bottom-modal" :class="modalName=='bottomModal'?'show':''">
				<view class="cu-dialog">
					<view class="cu-bar bg-white">
						<view class="action text-green" @tap="hideModal">确定</view>
						<view class="action text-blue" @tap="hideModal">取消</view>
					</view>
					<view class="">
						<radio-group class="block" v-for="(item, index) in this.bankList" v-key="index" @change="RadioChange">
							<view class="cu-form-group">
								<view class="padding-tb">
									<view class="title">{{item.bankName}}</view>
									<view class="desc text-sm">单笔限额{{item.singleAmount}},每日限额{{item.dayLimitAmount}}</view>
								</view>
								<radio :checked="index==currentIndex" value="A"></radio>
							</view>
						</radio-group>
					</view>
				</view>
			</view>
			<!--选择银行 end -->
		</view>
		
		<view class="padding flex flex-direction">
			<button class="cu-btn bg-red margin-tb-sm lg" @tap="doRecharge(e)">充值</button>
		</view>
		
	</view>
</template>

<script>
	var _this;

	import permision from "@/common/permission.js"

	import {
		mapMutations,
		mapGetters
	} from 'vuex';

	export default {
		data() {
			return {
				modalName: null,
				currentIndex: 0,
				bankList: []
			}
		},

		onLoad: function() {
			_this = this;

			this.queryBankList();
		},

		computed: {
			...mapGetters(["token", "userInfo"]),
		},

		methods: {
			...mapMutations(['updateToken', "setUserInfo"]),

			showModal(e) {
				this.modalName = e.currentTarget.dataset.target
			},
			hideModal(e) {
				this.modalName = null
			},

			RadioChange(e) {
				this.radio = e.detail.value
			},

			queryBankList: function() {
				uni.request({
					url: this.BASE_URL + '/bank/query/bankList',
					method: 'POST',
					header: {
						'Content-Type': 'application/x-www-form-urlencoded',
						'token': _this.token
					},
					data: {},
					success: (res) => {
						console.log(JSON.stringify(res));
						if (res.data.code == "B0000") {
							this.bankList = res.data.data;
							if (_this.bankList.length == 0) {
								_this.gotoAddBank();
							}
							_this.$token.updateToken(res.header.token);

						} else {
							console.log(res.data.msg)
						}
					},
					fail: (res) => {},
					complete: (res) => {
						uni.hideLoading();
					}
				});
			},

			doRecharge: function() {
				uni.request({
					url: this.BASE_URL + '/transfer/pay/BankCard2QbTransfer',
					method: 'POST',
					header: {
						'Content-Type': 'application/x-www-form-urlencoded',
						'token': _this.token
					},
					data: {
						payerAccountNbr: "",
						transferAmount: "",
						transferPassword: "",
						transferDesc: ""
					},
					success: (res) => {
						console.log(JSON.stringify(res));
						if (res.data.code == "B0000") {

							_this.$token.updateToken(res.header.token);

						} else {
							console.log(res.data.msg)
						}
					},
					fail: (res) => {},
					complete: (res) => {
						uni.hideLoading();
					}
				});
			},

			gotoAddBank() {
				uni.showModal({
					title: '提示',
					content: "请您先添加银行卡",
					showCancel: false,
					success: function(res) {
						if (res.confirm) {
							uni.navigateTo({
								url: '../addBankCard-01/addBankCard-01'
							})
						}
					}
				})
			},
		}
	}
</script>

<style>

</style>
