<template>
	<view>
		<view class="mglr4 myRowBetween">
			<view class="item flexRowBetween">
				<view class="ll">请选择{{sliderData.url&&sliderData.url!='1'?'贷款':''}}类型</view>
				<view class="rr" @click="seltTypeShow">
					<text class="fs13" :style="submitData.relation_id!=''?'color:black':'color:#999'">
					{{submitData.relation_id!=''?item:'请选择'}}</text>
					<image class="arrowR" src="../../static/images/consulting-icon.png" mode=""></image>
				</view>
			</view>
			<view class="item flexRowBetween" v-if="submitData.relation_id==3||submitData.relation_id==4">
				<view class="ll">公司名称</view>
				<view class="rr">
					<input type="text" v-model="submitData.passage1" placeholder="请输入" placeholder-class="placeholder" />
				</view>
			</view>
			<view class="item flexRowBetween">
				<view class="ll">资金需求(万元)</view>
				<view class="rr">
					<input type="number" v-model="submitData.keywords" placeholder="请输入" placeholder-class="placeholder" />
				</view>
			</view>
			<view class="item flexRowBetween">
				<view class="ll">联系人</view>
				<view class="rr">
					<input type="text" v-model="submitData.title" placeholder="请输入" placeholder-class="placeholder" />
				</view>
			</view>
			<view class="item flexRowBetween">
				<view class="ll">联系电话</view>
				<view class="rr">
					<input type="text" v-model="submitData.phone" placeholder="请输入" placeholder-class="placeholder" maxlength='11'/>
				</view>
			</view>
			
		</view>
		<view class="submitbtn" style="margin-top: 200rpx;">
			<button class="btn" type="button"  open-type="getUserInfo" @getuserinfo="Utils.stopMultiClick(submit)">提交</button>
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
				<view class="text this-text">{{sliderData.url&&sliderData.url!='1'?'贷款':''}}咨询</view>
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
				<view class="pdb10">个人{{sliderData.url&&sliderData.url!='1'?'贷款':''}}</view>
				<view class="flex fs12 color6">
					<view class="flex mgr20" @click="personCurr('1','个人消费贷款')">
						<image class="seltIcon" :src="curr==1?'../../static/images/icon1.png':'../../static/images/icon2.png'" mode=""></image>
						<span>个人消费{{sliderData.url&&sliderData.url!='1'?'贷款':''}}</span>
					</view>
					<view class="flex" @click="personCurr('2','个人经营贷款')">
						<image class="seltIcon" :src="curr==2?'../../static/images/icon1.png':'../../static/images/icon2.png'" mode=""></image>
						<span>个人经营{{sliderData.url&&sliderData.url!='1'?'贷款':''}}</span>
					</view>
				</view>
			</view>
			<view class="item borderB1">
				<view class="pdb10">企业{{sliderData.url&&sliderData.url!='1'?'贷款':''}}</view>
				<view class="flex fs12 color6">
					<view class="flex mgr20" @click="personCurr('3','商业贷款')">
						<image class="seltIcon" :src="curr==3?'../../static/images/icon1.png':'../../static/images/icon2.png'" mode=""></image>
						<span>商业{{sliderData.url&&sliderData.url!='1'?'贷款':''}}</span>
					</view>
					<view class="flex" @click="personCurr('4','政策性贷款')">
						<image class="seltIcon" :src="curr==4?'../../static/images/icon1.png':'../../static/images/icon2.png'" mode=""></image>
						<span>政策性{{sliderData.url&&sliderData.url!='1'?'贷款':''}}</span>
					</view>
				</view>
			</view>
			<view class="submitbtn pdlr4 mgt30 pdt15">
				<button class="btn" type="button" @click="confirm">确定</button>
			</view>
			
			
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
				showView: false,
				wx_info:{},
				is_show:false,
				is_seltTypeShow:false,
				curr:0,
				qiyeCurr:0,
				Router:this.$Router,
				Utils:this.$Utils,
				submitData:{
					type:1,
					title:'',
					phone:'',
					keywords:'',
					relation_id:'',
					behavior:'',
					passage1:''
				},
				item:'',
				sliderData:{}
			}
		},
		
		onLoad() {
			const self = this;
			self.$Utils.loadAll(['getSliderData'], self);
		},
		
		methods: {
			
			getSliderData() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					title:'首页轮播图',
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.sliderData = res.info.data[0]
						console.log('423423',self.sliderData)
					}
					self.$Utils.finishFunc('getSliderData');
				};
				self.$apis.labelGet(postData, callback);
			},
			
			submit() {
				const self = this;
				uni.setStorageSync('canClick', false);
				uni.showLoading({
					title: '提交中...',
					mask: true
				});
				var newObject = self.$Utils.cloneForm(self.submitData);
				if(self.submitData.relation_id==1||self.submitData.relation_id==2){
					delete newObject.passage1
				};
				const pass = self.$Utils.checkComplete(newObject);
				console.log('pass', pass);
				console.log('self.submitData',self.submitData)
				
				if (pass) {	
					const callback = (user, res) => {
						console.log(res)
						self.messageAdd();
					};
					self.$Utils.getAuthSetting(callback);
				
				} else {
					uni.setStorageSync('canClick', true);
					self.$Utils.showToast('请补全信息', 'none')
				};
			},
			
			messageAdd() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				if(!wx.getStorageSync('user_info')||!wx.getStorageSync('user_info').headImgUrl){
				  postData.refreshToken = true;
				};
				postData.data = {};
				postData.data = self.$Utils.cloneForm(self.submitData);
				const callback = (data) => {				
					if (data.solely_code == 100000) {					
						self.$Utils.showToast('提交成功', 'none', 1000)
						self.submitData = {
							type:1,
							title:'',
							phone:'',
							keywords:'',
							relation_id:'',
							behavior:'',
							passage1:''
						};
						self.item = '';
						self.curr = 0;
					} else {
						uni.setStorageSync('canClick', true);
						self.$Utils.showToast(data.msg, 'none', 1000)
					}	
				};
				self.$apis.messageAdd(postData, callback);
			},
			
			seltTypeShow(){
				const self = this;
				self.is_show = !self.is_show;
				self.is_seltTypeShow = !self.is_seltTypeShow
			},
			
			personCurr(curr,item){
				const self = this;
				if(curr!=self.curr){
					self.curr=curr;
					self.item = item;
					
					if(self.curr==1||self.curr==2){
						self.submitData.behavior = 	1
					}else if(self.curr==3||self.curr==4){
						self.submitData.behavior = 	2
					}
				}
			},
			
			confirm(){
				const self = this;
				self.seltTypeShow();
				self.submitData.relation_id = self.curr;
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
