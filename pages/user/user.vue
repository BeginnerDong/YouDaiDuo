<template>
	<view>
		<view class=""><image class="topBj" src="../../static/images/about-img.png" mode=""></image></view>
		
		<view class="flexColumn userBox">
			<view class="userPhoto"><image src="../../static/images/about-img1.png" mode=""></image></view>
			<view class="userName fs13 mgt5">哆啦A梦</view>
		</view>
		
		<view class="flexRowBetween myInfor pdlr4">
			<view class="item flex boxShaow" @click="Router.navigateTo({route:{path:'/pages/myLoan/myLoan'}})">
				<image class="icon" src="../../static/images/about-icon.png"></image>
				<view>我的贷款</view>
			</view>
			<view class="item flex boxShaow" @click="Router.navigateTo({route:{path:'/pages/myConsult/myConsult'}})">
				<image class="icon" src="../../static/images/about-icon1.png"></image>
				<view>我的咨询</view>
			</view>
		</view>
		
		<!--底部tab键-->
		<view class="navbar">
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">
				<view class="nav_img">
					<image src="../../static/images/nabar1.png" />
				</view>
				<view class="text">首页</view>
			</view>
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/consulting/consulting'}})">
				<view class="nav_img">
					<image src="../../static/images/nabar2.png" />
				</view>
				<view class="text">贷款咨询</view>
			</view>
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/user/user'}})" >
				<view class="nav_img">
					<image src="../../static/images/nabar3-a.png" />
				</view>
				<view class="text this-text">我的</view>
			</view>
		</view>
		<!--底部tab键 end-->
		
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
	@import "../../assets/style/navbar.css";
	page{padding-bottom: 140px;}
	
	.topBj{width: 100%;height: 250rpx;display: block;}
	.userBox{position: relative;margin-top: -90rpx;}
	.userPhoto{width: 130rpx;height: 130rpx;overflow: hidden;}
	.userPhoto image{width: 100%;height: 100%;display: block;border-radius: 50%;}
	
	.myInfor{margin-top:80rpx;}
	.myInfor .item{width: 48%;padding: 30rpx 4%;box-sizing: border-box;border-radius: 10rpx;}
	.myInfor .item .icon{width: 44rpx;height: 44rpx;margin-right: 10rpx;}
	
</style>
