<template>
	<view>
		
		<view class="pdlr4">
			<view class="banner-box">
				<view class="banner pdtb15">
					<swiper class="swiper-box" indicator-dots="true" autoplay="true" interval="3000" duration="1000" indicator-active-color="#fff">
						<block v-for="(item,index) in sliderData.mainImg" :key="index">
							<swiper-item class="swiper-item">
								<image :src="item.url" class="slide-image" />
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
						<swiper-item v-for="(item, index) in noticeData" :key="index">
							<navigator class="avoidOverflow" :data-id="item.id"
			@click="Router.navigateTo({route:{path:'/pages/informationDetail/informationDetail?id='+$event.currentTarget.dataset.id}})"
							>{{item.title}}</navigator>
						</swiper-item>
					</swiper>
				</view>
			</view>
		</view>
		<view class="f5H10"></view>
		
		<view class="indHome pdlr4 flex fs14 pdt15" v-show="sliderData.url&&sliderData.url!='1'">
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
			<button class="item" open-type="contact">
				<image src="../../static/images/home-icon4.png"></image>
				<view class="tit">在线客服</view>
			</button>
			<view class="item" @click="Router.navigateTo({route:{path:'/pages/aboutUs/aboutUs'}})">
				<image src="../../static/images/home-icon5.png"></image>
				<view class="tit">关于我们</view>
			</view>
			<view class="item" @click="Router.navigateTo({route:{path:'/pages/complaint/complaint'}})">
				<image src="../../static/images/home-icon6.png"></image>
				<view class="tit">投诉建议</view>
			</view>
		</view>
		<view class="f5H10" v-show="sliderData.url&&sliderData.url!='1'"></view>
		
		<view class="R-Fixbtn" @click="tel">
			<image class="icon" src="../../static/images/home-icon7.png" mode=""></image>
		</view>
		
		<view class="mglr4 pdtb15" v-show="sliderData.url&&sliderData.url!='1'">
			<view class="fs15 ftw pdb10">特色服务</view>
			<view class="flexRowBetween ind-service">
				<view class="Lpic item" v-if="serviceData[0]"
				@click="Router.navigateTo({route:{path:'/pages/consultDetail/consultDetail?id='+serviceData[0].id+'&title='+serviceData[0].title}})">
					<image :src="serviceData&&serviceData[0]&&serviceData[0].mainImg&&
					serviceData[0].mainImg[0]?serviceData[0].mainImg[0].url:''" mode=""></image>
					<view class="text flexCenter">{{serviceData&&serviceData[0]?serviceData[0].title:''}}</view>
				</view>
				<view class="R-TwoPic">
					<view class="item mgb10" v-if="serviceData[1]"
					@click="Router.navigateTo({route:{path:'/pages/consultDetail/consultDetail?id='+serviceData[1].id+'&title='+serviceData[1].title}})">
						<image :src="serviceData&&serviceData[1]&&serviceData[1].mainImg&&
					serviceData[1].mainImg[0]?serviceData[1].mainImg[0].url:''" mode=""></image>
						<view class="text flexCenter">{{serviceData&&serviceData[1]?serviceData[1].title:''}}</view>
					</view>
					<view class="item" v-if="serviceData[2]"
					@click="Router.navigateTo({route:{path:'/pages/consultDetail/consultDetail?id='+serviceData[2].id+'&title='+serviceData[2].title}})">
						<image :src="serviceData&&serviceData[2]&&serviceData[2].mainImg&&
					serviceData[2].mainImg[0]?serviceData[2].mainImg[0].url:''" mode=""></image>
						<view class="text flexCenter">{{serviceData&&serviceData[2]?serviceData[2].title:''}}</view>
					</view>
				</view>
			</view>
		</view>
		<view class="f5H10" v-show="sliderData.url&&sliderData.url!='1'"></view>
		
		<view class="pdlr4 pdt15">
			<view class="zixunNav flex fs13 color6">
				<view class="tt mgr20" :class="curr==1?'on':''" @click="changeCurr('1')">企业福利</view>
				<view class="tt" :class="curr==2?'on':''" @click="changeCurr('2')">健康资讯</view>
			</view>
			<view class="zixunList">
				<view class="item flexRowBetween" v-for="(item,index) in mainData" :key="index" :data-id="item.id"
				@click="Router.navigateTo({route:{path:'/pages/newsDetail/newsDetail?id='+$event.currentTarget.dataset.id}})">
					<view class="ll"><image :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''" mode=""></image></view>
					<view class="rr">
						<view class="tit fs13 avoidOverflow2">
							{{item.title}}
						</view>
						<view class="time color9 fs10">{{item.create_time}}</view>
					</view>
				</view>
			</view>
		</view>
		
		<!--底部tab键-->
		<view class="navbar"  v-show="sliderData.url&&sliderData.url!='1'" >
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
				zixunData:[{},{},{},{}],
				sliderData:{},
				noticeData:[],
				serviceData:[],
				getBefore:{
					article:{
						tableName:'Label',
						middleKey:'menu_id',
						key:'id',
						searchItem:{
							title: ['in', ['行业资讯']],
						},
						condition:'in'
					}
				},
				mainData:[]
			}
		},
		
		onLoad() {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			self.$Utils.loadAll(['getPhoneData','getServiceData','getSliderData','getNoticeData','getMainData'], self);
		},
		
		onReachBottom() {
			console.log('onReachBottom')
			const self = this;
			if (!self.isLoadAll && uni.getStorageSync('loadAllArray')) {
				self.paginate.currentPage++;
				self.getMainData()
			};
		},
		
		methods: {
			
			getMainData(isNew) {
				const self = this;
				if (isNew) {
					self.mainData = [];
					self.paginate = {
						count: 0,
						currentPage: 1,
						is_page: true,
						pagesize: 10
					}
				};
				const postData = {};
				postData.searchItem = {
					thirdapp_id:2
				};
				postData.paginate = self.$Utils.cloneForm(self.paginate);
				postData.getBefore = self.$Utils.cloneForm(self.getBefore)
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData,res.info.data)
					}
					console.log(self.noticeData)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.articleGet(postData, callback);
			},
			
			getServiceData(){
			    var self = this;
			    var postData = {};
			    postData.searchItem = {
					thirdapp_id:2,
				};
				postData.getBefore = {
					child:{
						tableName:'Label',
						middleKey:'parentid',
						key:'id',
						searchItem:{
							status:['in',[1]],
							title:['in',['特色服务']]
						},
						condition:'in',
					}
				};
				postData.order = {
					listorder:'desc'
				};
			    var callback = function(res){
			        if(res.info.data.length>0&&res.info.data[0]){
						self.serviceData.push.apply(self.serviceData,res.info.data)
			        };   
					 console.log(res)
					self.$Utils.finishFunc('getServiceData');
			    };
				self.$apis.labelGet(postData, callback);
			},
			
			
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
			
			getNoticeData() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					thirdapp_id:2
				};
				postData.getBefore = {
					article:{
						tableName:'Label',
						middleKey:'menu_id',
						key:'id',
						searchItem:{
							title: ['in', ['首页广告']],
						},
						condition:'in'
					}
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.noticeData.push.apply(self.noticeData,res.info.data)
					}
					console.log(self.noticeData)
					self.$Utils.finishFunc('getNoticeData');
				};
				self.$apis.articleGet(postData, callback);
			},
			
			changeCurr(curr){
				const self = this;
				if(curr!=self.curr){
					self.curr = curr;
					if(self.curr==1){
						self.getBefore = {
							article:{
								tableName:'Label',
								middleKey:'menu_id',
								key:'id',
								searchItem:{
									title: ['in', ['行业资讯']],
								},
								condition:'in'
							}
						}
					}else if(self.curr==2){
						self.getBefore = {
							article:{
								tableName:'Label',
								middleKey:'menu_id',
								key:'id',
								searchItem:{
									title: ['in', ['贷款资讯']],
								},
								condition:'in'
							}
						}
					};
					self.getMainData(true)
				}
			},
			
			getPhoneData() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					thirdapp_id:2
				};
				postData.getBefore = {
					article:{
						tableName:'Label',
						middleKey:'menu_id',
						key:'id',
						searchItem:{
							title: ['in', ['关于我们']],
						},
						condition:'in'
					}
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.phoneData = res.info.data[0];
					};
					console.log(self.mainData)
					self.$Utils.finishFunc('getPhoneData');
				};
				self.$apis.articleGet(postData, callback);
			},
			//拨打电话
			tel(){
				const self = this;
				uni.makePhoneCall({
					phoneNumber: self.phoneData.title //仅为示例
				});
			},
			
		}
	};
</script>

<style>
	@import "../../assets/style/navbar.css";
	@import "../../assets/style/index.css";
	
	page {padding-bottom: 140rpx;}

	button{
		background: none;
		line-height: 1.5;
	}
	button::after{
		border: none;
	}
	.button-hover{
		color: #000000;
		background: none;
	}
</style>
