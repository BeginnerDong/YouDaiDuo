<template>
	<view>
		<view class="orderNav flexRowBetween whiteBj">
			<view class="tt" v-for="item in serviceData" :class="num==item.id?'on':''" 
			@click="changeNum(item.id,item.art[0].id)">{{item.title}}</view>
			
		</view>
		<view class="pdtb20"></view>
		
		<view class="mglr4 myLoanList fs13 mgt15" v-if="mainData.length>0">
			<view class="item" v-for="(item,index) in mainData" :key="index">
				<view class="oneLine flexRowBetween">
					<view class="">咨询时间：{{item.create_time}}</view>
					<view class="color6 flexEnd" @click="messageUpdate(item.id)">
						<image class="delIcon" src="../../static/images/my-advice-icon.png" mode="">
							
						</image>删除</view>
				</view>
				<view class="pdlr4 mgt10">{{item.description}}</view>
			</view>
		</view>
		
		<view class="mglr4 myLoanList fs13 mgt15" v-if="mainData.length==0">
			<view class="nodata flexCenter"><image src="../../static/images/nodata.png" mode="widthFix"></image></view>
		</view>
		
		
		<view class="black-bj" v-show="is_show"></view>
		<view class="alertShow center whiteBj radius10 pdt20" v-show="is_alertShow">
			<view class="tip-title mgb10 fs15">提示</view>
			<view class="fs13 color6 pdb20 borderB1">是否确认删除该条咨询？</view>
			<view class="flex tip-button">
				<view class="item"  @click="alertShow">取消</view>
				<view class="item pubColor">确定</view>
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
				loanData:[{},{}],
				is_alertShow:false,
				num:-1,
				serviceData:[],
				mainData:[]
			}
		},
		
		onLoad() {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			self.$Utils.loadAll(['getServiceData'], self);
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
			changeNum(num,id){
				const self=this;
				if(num!=self.num){
					self.num = num
					self.art_id = id;
					self.getMainData(true)
				}
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
				postData.getAfter = {
					art:{
						tableName:'Article',
						middleKey:'id',
						key:'menu_id',
						searchItem:{
							status:1
						},
						condition:'='
					}	
				};
			    var callback = function(res){
			        if(res.info.data.length>0&&res.info.data[0]){
						self.serviceData.push.apply(self.serviceData,res.info.data);
						self.num = self.serviceData[0].id;
						self.art_id = self.serviceData[0].art[0].id;
						self.getMainData()
			        };    
					
			    };
				self.$apis.labelGet(postData, callback);
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
				postData.searchItem = {
					relation_id:self.art_id
				};
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
					self.$Utils.finishFunc('getServiceData');
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
