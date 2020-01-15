<template>
	<view>
		
		<view class="detailxqBan" style="height: 400rpx;">
			<image src="../../static/images/about-us-img.png" mode=""></image>
		</view>
		<view class="mglr4 adrsLis">
			<view class="item borderB1">
				<image class="icon" src="../../static/images/about-us-icon2.png" mode=""></image>
				<view>15623266556</view>
			</view>
			<view class="item">
				<image class="icon" src="../../static/images/about-us-icon1.png" mode=""></image>
				
				<view>陕西省西安市雁塔区高新大都荟</view>
			</view>
		</view>
		<view class="f5H10"></view>
		<view class="mglr4 pdtb15">
			<view class="ftw fs15 pdb10">关于我们</view>
			<view class="xqInfor">
				<view class="cont fs13">
					<view>和公交卡分类时段海格力斯过会就客服电话鬼斧神工和发换个飞机口袋里还股份第三个和付赛供货方度高刚发的刚发就是个好人撒刚发的省挂号费数据库规划局分雕刻时光发几个好供货方接口上的</view>
					<view>估计快了单方事故了供货方加快代领很过分四大皆空供货方度高话估计发过火供货方就看看的火锅</view>
				</view>
			</view>
			
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				showView: false,
				wx_info:{},
				is_show:false
			}
		},
		
		onLoad() {
			const self = this;
			// self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			getMainData() {
				const self = this;
				console.log('852369')
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				self.$apis.orderGet(postData, callback);
			}
		}
	};
</script>

<style>
	@import "../../assets/style/detial.css";
	.adrsLis .item{padding: 30rpx 0;align-items: flex-start;padding-left: 50rpx;position: relative;}
	.adrsLis .item .icon{width: 36rpx;height: 36rpx; display: block;position: absolute;top: 30rpx;left: 0;}
	.xqInfor{line-height: 44rpx;}
</style>
