<template>
	<view>
		<view class="mglr4 myRowBetween">
			<view class="item flexRowBetween">
				<view class="ll">请选择贷款类型</view>
				<view class="rr" @click="seltTypeShow">
					<text class="color9 fs13">请选择</text>
					<image class="arrowR" src="../../static/images/consulting-icon.png" mode=""></image>
				</view>
			</view>
			<view class="item flexRowBetween">
				<view class="ll">公司名称</view>
				<view class="rr">
					<input type="number" value="" placeholder="请输入" placeholder-class="placeholder" />
				</view>
			</view>
			<view class="item flexRowBetween">
				<view class="ll">资金需求(万元)</view>
				<view class="rr">
					<input type="number" value="" placeholder="请输入" placeholder-class="placeholder" />
				</view>
			</view>
			<view class="item flexRowBetween">
				<view class="ll">联系人</view>
				<view class="rr">
					<input type="text" value="" placeholder="请输入" placeholder-class="placeholder" />
				</view>
			</view>
			<view class="item flexRowBetween">
				<view class="ll">联系电话</view>
				<view class="rr">
					<input type="text" value="" placeholder="请输入" placeholder-class="placeholder" maxlength='11'/>
				</view>
			</view>
			
		</view>
		<view class="submitbtn" style="margin-top: 200rpx;">
			<button class="btn" type="button">提交</button>
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
					<image src="../../static/images/nabar2-a.png" />
				</view>
				<view class="text this-text">贷款咨询</view>
			</view>
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/user/user'}})" >
				<view class="nav_img">
					<image src="../../static/images/nabar3.png" />
				</view>
				<view class="text">我的</view>
			</view>
		</view>
		<!--底部tab键 end-->
		
		<view class="black-bj" v-show="is_show"></view>
		
		<view class="seltTypeShow" v-show="is_seltTypeShow">
			<view class="closebtn" @click="seltTypeShow">×</view>
			<view class="item borderB1">
				<view class="pdb10">个人贷款</view>
				<view class="flex fs12 color6">
					<view class="flex mgr20" @click="personCurr('1')">
						<image class="seltIcon" :src="curr==1?'../../static/images/icon1.png':'../../static/images/icon2.png'" mode=""></image>
						<span>个人消费贷款</span>
					</view>
					<view class="flex" @click="personCurr('2')">
						<image class="seltIcon" :src="curr==2?'../../static/images/icon1.png':'../../static/images/icon2.png'" mode=""></image>
						<span>个人经营贷款</span>
					</view>
				</view>
			</view>
			<view class="item borderB1">
				<view class="pdb10">企业贷款</view>
				<view class="flex fs12 color6">
					<view class="flex mgr20" @click="enterpriseCurr('1')">
						<image class="seltIcon" :src="qiyeCurr==1?'../../static/images/icon1.png':'../../static/images/icon2.png'" mode=""></image>
						<span>商业贷款</span>
					</view>
					<view class="flex" @click="enterpriseCurr('2')">
						<image class="seltIcon" :src="qiyeCurr==2?'../../static/images/icon1.png':'../../static/images/icon2.png'" mode=""></image>
						<span>政策性贷款</span>
					</view>
				</view>
			</view>
			<view class="submitbtn pdlr4 mgt30 pdt15">
				<button class="btn" type="button">确定</button>
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
				is_show:false,
				is_seltTypeShow:false,
				curr:0,
				qiyeCurr:0
			}
		},
		
		onLoad() {
			const self = this;
			// self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			seltTypeShow(){
				const self = this;
				self.is_show = !self.is_show;
				self.is_seltTypeShow = !self.is_seltTypeShow
			},
			personCurr(curr){
				const self = this;
				if(curr!=self.curr){
					self.curr=curr
				}
			},
			enterpriseCurr(qiyeCurr){
				const self = this;
				if(qiyeCurr!=self.qiyeCurr){
					self.qiyeCurr=qiyeCurr
				}
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
	@import "../../assets/style/editInfor.css";
	page{padding-bottom: 140px;}
	
	.seltTypeShow{position: fixed;top: 50%;left: 50%;transform: translate(-50%,-50%);z-index: 45;width: 80%;background: #fff;border-radius: 10rpx;padding-bottom: 80rpx;}
	.seltTypeShow .item{border-bottom: 1px solid #eee;padding: 30rpx 4%;}
	.seltIcon{width:28rpx;height: 28rpx;margin-right: 10rpx;}
</style>
