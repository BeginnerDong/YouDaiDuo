<template>
	<view>
		<view class="orderNav flexRowBetween whiteBj">
			<view class="tt" :class="num==1?'on':''" @click="changeNum('1')">个人{{sliderData.url&&sliderData.url!='1'?'贷款':''}}</view>
			<view class="tt" :class="num==2?'on':''" @click="changeNum('2')">企业{{sliderData.url&&sliderData.url!='1'?'贷款':''}}</view>
		</view>
		<view class="pdtb20"></view>
		
		<view class="mglr4 myLoanList fs13 mgt15" v-if="mainData.length>0">
			<view class="item" v-for="(item,index) in mainData" :key="index">
				<view class="oneLine flexRowBetween">
					<view class="">咨询时间：{{item.create_time}}</view>
					<view class="color6 flexEnd" @click="messageUpdate(item.id)">
						<image class="delIcon" src="../../static/images/my-advice-icon.png" mode=""></image>
						删除</view>
				</view>
				<view class="pdlr4">
					<view class="line">资金需求：{{item.keywords}}</view>
					<view class="line">联系人：{{item.title}}</view>
					<view class="line">联系电话：{{item.phone}}</view>
					<view class="line pubColor">{{item.art&&item.art[0]&&item.art[0].label&&item.art[0].label[item.art[0].menu_id]?item.art[0].label[item.art[0].menu_id].title:''}}</view>
				</view>
			</view>
		</view>
		
		<view class="mglr4 myLoanList fs13 mgt15" v-if="mainData.length==0">
			<view class="nodata flexCenter"><image src="../../static/images/nodata.png" mode="widthFix"></image></view>
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
				loanData:[{},{}],
				is_alertShow:false,
				num:1,
				mainData:[],
				searchItem:{
					type:1,
					thirdapp_id:2,
					behavior:1
				},
				sliderData:{}
			}
		},
		
		onLoad() {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			self.$Utils.loadAll(['getMainData','getSliderData'], self);
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
			
			changeNum(num){
				const self=this;
				if(num!=self.num){
					self.num = num;
					self.searchItem.behavior = self.num;
					self.getMainData(true)
				}
			},
			
			alertShow(){
				const self=this;
				self.is_alertShow = !self.is_alertShow;
				self.is_show = !self.is_show;
			},
			
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
				postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = self.$Utils.cloneForm(self.searchItem);
				postData.paginate = self.$Utils.cloneForm(self.paginate);
				postData.getAfter = {
					art:{
						tableName:'Article',
						middleKey:'relation_id',
						key:'id',
						searchItem:{
							status:1
						},
						condition:'='
					}	
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData,res.info.data)
					}
					console.log(self.noticeData)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.messageGet(postData, callback);
			},
			
			messageUpdate(id) {
				const self = this;
				uni.showModal({
					title: '提示',
					content: '是否确认删除该条记录？',
					confirmColor:'#fb4856',
					success: (res)=>{
						if (res.confirm) {
							const postData = {};
							postData.tokenFuncName = 'getProjectToken';
							postData.data = {
								status:-1
							};
							postData.searchItem = {
								id:id,
							};
							const callback = (data) => {
								uni.setStorageSync('canClick', true);
								if (data && data.solely_code == 100000) {
									self.$Utils.showToast('操作成功','none');
									setTimeout(function() {
										self.getMainData(true)
									}, 1000);
								} else {
									self.$Utils.showToast(data.msg,'none')
								}
							};
							self.$apis.messageUpdate(postData, callback);
						} else if (res.cancel) {
							console.log('用户点击取消');
						}
					}
				});
			},
		}
	};
</script>

<style>
	@import "../../assets/style/orderNav.css";
	@import "../../assets/style/myOrder.css";
	page{background: #F5F5F5;padding-bottom:60px;}
	
</style>
