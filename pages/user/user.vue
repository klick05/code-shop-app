<template>
	<view class="user">
		<!-- 头部 -->
		<view class="user-wrap" @click="tologin()">
			<view class="setting iconfont icon31shezhi"></view>
			<view class="info">
				<image class="avatar" mode="aspectFill" :src="userInfo.memberAvatar||userInfo.wxHeadImg||conf.defaultImg"></image>
				<view class="nickname">{{ userInfo.wxNickName||userInfo.memberName }}
					<text v-if="userInfo.level==100" style="color: red;"></text>
					<text v-if="userInfo.level==101" style="color: red;">·会员</text>
				</view>
			</view>
		</view>

		<!-- 订单状态 -->
		<view class="order-status">
			<view class="status-wrap">
				<!-- 单元格 -->
				<view class="cell" @click="$navigateTo('/pages/order/order')">
					<view class="cell-left">
						<image class="cell-icon" src="/static/img/user/icon-order.png" mode="aspectFill"></image>
						<view class="cell-text">全部订单</view>
					</view>
					<view class="iconfont iconmore1"></view>
				</view>

				<!-- 订单状态 -->
				<view class="status-list">
					<view class="status-item" hover-class="btn-hover" v-for="(item, index) in orderStatusList" :key="index">
						<min-badge :count="item.count">
							<view class="item-icon" :class="item.icon" @click="$navigateTo('/pages/order/order?stat=' + item.status)"></view>
							<view class="item-text">{{ item.name }}</view>
						</min-badge>
					</view>
				</view>
			</view>
		</view>

		<!-- 用户功能 -->
		<view class="com-item">
			<view class="com-wrap">

				<view class="cell" @click="tuiguang()" >
					<view class="cell-left">
						<image class="cell-icon" src="/static/img/user/icon-foot.png" mode="aspectFill"></image>
						<view class="cell-text">我的推荐码</view>
					</view>
					<view class="iconfont iconmore1"></view>
				</view>


				<view class="cell" @click="$navigateTo('/pages/user/subordinate')" >
					<view class="cell-left">
						<image class="cell-icon" src="/static/img/user/icon-collect.png" mode="aspectFill"></image>
						<view class="cell-text">推荐记录</view>
					</view>
					<view class="iconfont iconmore1"></view>
				</view>


				<view class="cell" @click="$navigateTo('/pages/user/fumou-center-template')" >
					<view class="cell-left">
						<image class="cell-icon" src="/static/img/user/icon-about.png" mode="aspectFill"></image>
						<view class="cell-text">我的奖金</view>
					</view>
					<view class="iconfont iconmore1"></view>
				</view>
				<view class="cell" @click="$navigateTo('/pages/user/commission')" >
					<view class="cell-left">
						<image class="cell-icon" src="/static/img/user/icon-foot.png" mode="aspectFill"></image>
						<view class="cell-text">奖金记录</view>
					</view>
					<view class="iconfont iconmore1"></view>
				</view>

			</view>
		</view>

		<!-- 用户服务 -->
		<view class="com-item">
			<view class="com-wrap">
				<view class="cell" @click="$navigateTo('/pages/order/order-refund')">
					<view class="cell-left">
						<image class="cell-icon" src="/static/img/user/icon-kefu.png" mode="aspectFill"></image>
						<view class="cell-text">售后记录</view>
					</view>
					<view class="iconfont iconmore1"></view>
				</view>
				
				<view class="cell" @click="$navigateTo('/pages/address/address')">
					<view class="cell-left">
						<image class="cell-icon" src="/static/img/user/icon-address.png" mode="aspectFill"></image>
						<view class="cell-text">收货地址</view>
					</view>
					<view class="iconfont iconmore1"></view>
				</view>


				<view class="cell">
					<view class="cell-left">
						<image class="cell-icon" src="/static/img/user/icon-kefu.png" mode="aspectFill"></image>
						<view class="cell-text">客服中心</view>
					</view>
					<view class="iconfont iconmore1"></view>
				</view>

				<view class="cell" @click="$navigateTo('/pages/user/collect')">
					<view class="cell-left">
						<image class="cell-icon" src="/static/img/user/icon-collect.png" mode="aspectFill"></image>
						<view class="cell-text">我的收藏</view>
					</view>
					<view class="iconfont iconmore1"></view>
				</view>

				<view class="cell">
					<view class="cell-left">
						<image class="cell-icon" src="/static/img/user/icon-help.png" mode="aspectFill"></image>
						<view class="cell-text">帮助中心</view>
					</view>
					<view class="iconfont iconmore1"></view>
				</view>
				<view class="cell" @click="$navigateTo('/pages/user/html?key=cfg_rej_pocy')">
					<view class="cell-left">
						<image class="cell-icon" src="/static/img/user/icon-help.png" mode="aspectFill"></image>
						<view class="cell-text">退货政策</view>
					</view>
					<view class="iconfont iconmore1"></view>
				</view>

				<view class="cell" @click="$navigateTo('/pages/user/html?key=cfg_call_us')">
					<view class="cell-left">
						<image class="cell-icon" src="/static/img/user/icon-about.png" mode="aspectFill"></image>
						<view class="cell-text">联系我们</view>
					</view>
					<view class="iconfont iconmore1"></view>
				</view>

				<view class="cell" @click="$navigateTo('/pages/user/html?key=cfg_how_tobuy')">
					<view class="cell-left">
						<image class="cell-icon" src="/static/img/user/icon-collect.png" mode="aspectFill"></image>
						<view class="cell-text">如何购买</view>
					</view>
					<view class="iconfont iconmore1"></view>
				</view>

				<view class="cell" @click="$navigateTo('/pages/user/html?key=cfg_com_help')">
					<view class="cell-left">
						<image class="cell-icon" src="/static/img/user/icon-about.png" mode="aspectFill"></image>
						<view class="cell-text">帮助中心</view>
					</view>
					<view class="iconfont iconmore1"></view>
				</view>


			</view>
		</view>
	</view>
</template>

<script>
	import minBadge from '@/components/min-badge/min-badge'
	export default {
		components: {
			minBadge
		},
		data() {
			let _conf = this.getConst();

			return {
				conf: _conf,

				userInfo: {
					//headImg: '/static/img/user/avatar.jpg',
					headImg: '/static/img/user/default-head.png',
					nickName: 'noname'
				},
				orderStatusList: [{
						name: '待付款',
						icon: 'iconfont icon31daifukuan',
						status: 1,
						count: 0
					},
					{
						name: '待发货',
						icon: 'iconfont icon31daifahuo',
						status: 2,
						count: 0
					},
					{
						name: '待收货',
						icon: 'iconfont icon31daishouhuo',
						status: 3,
						count: 0
					},
					{
						name: '待评价',
						icon: 'iconfont icon31daipingjia',
						status: 6,
						count: 0
					},
					{
						name: '已完成',
						icon: 'iconfont icon31yiguanzhudianpu',
						status: 4,
						count: 0
					}
				],
				currentIndex: 0,
			};
		},
		methods: {
			tuiguang() {
				var user = this.$dataLocal("user_info") || {};
				var _url = "./external/guider.html?guider=" + user.id;
				if (this.isWeixin()) {
					location.href = _url
				} else {
					this.$navigateTo(`/pages/user/zhiwen-share`);
				}
			},
			tologin() {
				if (this.$isNull(this.userInfo.memberId) || this.$isNull(this.userInfo.memberPhone)) {
					//this.$register("/pages/user/user","$switchTab")
					this.$dataLocal("pre_reg_page", "/pages/user/user");
					this.$navigateTo("/pages/login/register");

				} else {
					this.$navigateTo("/pages/user/set")
				}
			},
			getuser() {
				let _user = this.userInfo;
				let user = this.$dataLocal("user_info");
				if(this.$isNull(user)){
					this.$navigateTo("/pages/login/login");
				}else{
					this.userInfo = user
				}
			},
			getOrderStatusCount() {
				uni.request({
					url: 'http://localhost:8888/codeworld-order/get-order-status-count',
					method: 'POST',
					header: {
						'token': this.$dataLocal('token')
					},
					success: (response) => {
						if (response.data.code === 20000) {
							let data = response.data.data;
							for (let index in this.orderStatusList) {
								let orderStatus = this.orderStatusList[index]
								switch (orderStatus.status) {
									case 1:
										orderStatus.count = data.pendingPaymentCount;
										break;
									case 2:
										orderStatus.count = data.toBeDeliveredCount;
										break;
									case 3:
										orderStatus.count = data.toBeReceivedCount;
										break;
									case 4:
										orderStatus.count = data.completedCount;
										break;
									case 6:
										orderStatus.count = data.comment;
										break;
								}
							}
						}
					}
				})
			}
		},
		onLoad() {
			this.getuser();
		},
		onShow() {
			this.getOrderStatusCount()
		}
	};
</script>

<style lang="scss">
	//@import "../../static/css/iconfont/iconfont.css";

	page {
		background: #f2f2f2;
	}

	.btn-hover {
		background: #f2f2f2 !important;
	}

	.user {
		.user-wrap {
			display: flex;
			justify-content: center;
			align-items: center;
			height: 50vw;
			padding: 30rpx;
			z-index: 9;
			border-radius: 0 0 20% 20%;
			background: url('https://handsel.oss-cn-shenzhen.aliyuncs.com/1588938371592.jpg') no-repeat;
			background-size: cover;

			.setting {
				color: #fff;
				position: absolute;
				top: 60rpx;
				left: 60rpx;
				font-size: 50rpx;
			}

			.info {
				position: absolute;
				text-align: center;



				/* #ifndef H5 */
				top: 10%;

				/* #endif */


				.avatar {
					width: 150rpx;
					height: 150rpx;
					border-radius: 50%;
				}

				.nickname {
					color: #fff;
					font-size: 28rpx;
				}
			}
		}

		.order-status {
			padding: 0 20rpx;
			margin-top: -10vw;

			.status-wrap {
				border-radius: 25rpx;
				overflow: hidden;

				.status-list {
					display: flex;
					justify-content: space-evenly;
					align-items: center;
					background: #fff;
					padding-top: 30rpx;
					padding-bottom: 30rpx;

					.status-item {
						flex: 1;
						display: flex;
						flex-direction: column;
						justify-content: center;
						align-items: center;

						.item-icon {
							line-height: 1;
							font-size: 65rpx;
							color: #bbb;
						}

						.item-text {
							font-size: 28rpx;
							color: #666;
							margin-top: 5rpx;
						}
					}
				}
			}
		}

		.com-item {
			padding-left: 20rpx;
			padding-right: 20rpx;
			margin-top: 20rpx;

			.com-wrap {
				border-radius: 25rpx;
				overflow: hidden;
			}
		}

		.cell {
			height: 80rpx;
			padding-left: 20rpx;
			padding-right: 20rpx;
			display: flex;
			justify-content: space-between;
			align-items: center;
			background: #fff;
			border-bottom: 1px solid #f8f8f8;

			&:active {
				background: #f2f2f2;
			}

			&:last-child {
				border-bottom: none !important;
			}

			.cell-left {
				display: flex;
				align-items: center;

				.cell-icon {
					width: 50rpx;
					height: 50rpx;
				}

				.cell-text {
					color: #666;
					font-size: 28rpx;
					margin-left: 20rpx;
				}
			}

			.iconfont {
				font-size: 40rpx;
				color: #999;
			}
		}
	}
</style>
