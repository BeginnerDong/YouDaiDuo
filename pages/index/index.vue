<template>
	<view>
		
		<view class="pdlr4">
			<view class="banner-box">
				<view class="banner pdtb15">
					<swiper class="swiper-box" indicator-dots="true" autoplay="true" interval="3000" duration="1000" indicator-active-color="#fff">
						<block v-for="(item,index) in labelData" :key="index">
							<swiper-item class="swiper-item">
								<image :src="item" class="slide-image" />
							</swiper-item>
						</block>
					</swiper>
				</view>
			</view>
			<view class="noticeLis flex pdb10">
				<view class="Licon mgr10">
					<image src="../../static/images/home-icon.png" mode=""></image>
				</view>
				<view class="rr fs13 color6">
					<swiper vertical="true" autoplay="true" circular="true" interval="3000">
						<swiper-item v-for="(item, index) in msg" :key="index">
							<navigator class="avoidOverflow">{{item}}</navigator>
						</swiper-item>
					</swiper>
				</view>
			</view>
		</view>
		<view class="f5H10"></view>
		
		<view class="indHome pdlr4 flex fs14 pdt15">
			<view class="item"  @click="Router.navigateTo({route:{path:'/pages/personalLoan/personalLoan'}})">
				<image src="../../static/images/home-icon1.png"></image>
				<view class="tit">个人贷款</view>
			</view>
			<view class="item" @click="Router.navigateTo({route:{path:'/pages/enterpriseLoan/enterpriseLoan'}})">
				<image src="../../static/images/home-icon2.png"></image>
				<view class="tit">企业贷款</view>
			</view>
			<view class="item" @click="Router.navigateTo({route:{path:'/pages/information/information'}})">
				<image src="../../static/images/home-icon3.png"></image>
				<view class="tit">贷款资讯</view>
			</view>
			<view class="item"  @click="Router.navigateTo({route:{path:'/pages//'}})">
				<image src="../../static/images/home-icon4.png"></image>
				<view class="tit">在线客服</view>
			</view>
			<view class="item" @click="Router.navigateTo({route:{path:'/pages/aboutUs/aboutUs'}})">
				<image src="../../static/images/home-icon5.png"></image>
				<view class="tit">关于我们</view>
			</view>
			<view class="item" @click="Router.navigateTo({route:{path:'/pages/complaint/complaint'}})">
				<image src="../../static/images/home-icon6.png"></image>
				<view class="tit">投诉建议</view>
			</view>
		</view>
		<view class="f5H10"></view>
		
		<view class="R-Fixbtn" @click="tel">
			<image class="icon" src="../../static/images/home-icon7.png" mode=""></image>
		</view>
		
		<view class="mglr4 pdtb15">
			<view class="fs15 ftw pdb10">特色服务</view>
			<view class="flexRowBetween ind-service">
				<view class="Lpic item" @click="Router.navigateTo({route:{path:'/pages/consultDetail/consultDetail'}})">
					<image src="../../static/images/home-img.png" mode=""></image>
					<view class="text flexCenter">财务咨询</view>
				</view>
				<view class="R-TwoPic">
					<view class="item mgb10" @click="Router.navigateTo({route:{path:'/pages/consultDetail/consultDetail'}})">
						<image src="../../static/images/home-img1.png" mode=""></image>
						<view class="text flexCenter">税务咨询</view>
					</view>
					<view class="item" @click="Router.navigateTo({route:{path:'/pages/consultDetail/consultDetail'}})">
						<image src="../../static/images/home-img1.png" mode=""></image>
						<view class="text flexCenter">法律咨询</view>
					</view>
				</view>
			</view>
		</view>
		<view class="f5H10"></view>
		
		<view class="pdlr4 pdt15">
			<view class="zixunNav flex fs13 color6">
				<view class="tt mgr20" :class="curr==1?'on':''" @click="changeCurr('1')">行业资讯</view>
				<view class="tt" :class="curr==2?'on':''" @click="changeCurr('2')">贷款资讯</view>
			</view>
			<view class="zixunList">
				<view class="item flexRowBetween" v-for="(item,index) in zixunData" :key="index" @click="Router.navigateTo({route:{path:'/pages/newsDetail/newsDetail'}})">
					<view class="ll"><image src="../../static/images/home-img2.png" mode=""></image></view>
					<view class="rr">
						<view class="tit fs13 avoidOverflow2">夫妻因婚外情离婚，无过错方可以向对方要多少精神损害赔偿?</view>
						<view class="time color9 fs10">2020.01.14</view>
					</view>
				</view>
			</view>
		</view>
		
		<!--底部tab键-->
		<view class="navbar">
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">
				<view class="nav_img">
					<image src="../../static/images/nabar1-a.png" />
				</view>
				<view class="text this-text">首页</view>
			</view>
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/consulting/consulting'}})">
				<view class="nav_img">
					<image src="../../static/images/nabar2.png" />
				</view>
				<view class="text">贷款咨询</view>
			</view>
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/user/user'}})" >
				<view class="nav_img">
					<image src="../../static/images/nabar3.png" />
				</view>
				<view class="text">我的</view>
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
				is_show:false,
				labelData: [
					"../../static/images/home-banner.png",
					"../../static/images/home-banner.png"
				],
				msg:[
					'uni-app行业峰会频频亮相，开发者反响热烈通知公告',
					'DCloud完成B2轮融资，uni-app震撼发布热烈通知公告热烈通知公告',
					'36氪热文榜推荐、CSDN公号推荐 DCloud CEO文章热烈通知公告热烈通知公告'
				],
				curr:1,
				zixunData:[{},{},{},{}]
			}
		},
		
		onLoad() {
			const self = this;
			// self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			changeCurr(curr){
				const self = this;
				if(curr!=self.curr){
					self.curr = curr
				}
			},
			//拨打电话
			tel(){
				uni.makePhoneCall({
					phoneNumber: '18932145667' //仅为示例
				});
			},
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
	@import "../../assets/style/index.css";
	
	page {padding-bottom: 140rpx;}

	
</style>
