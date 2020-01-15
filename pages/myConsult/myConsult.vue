<template>
	<view>
		<view class="orderNav flexRowBetween whiteBj">
			<view class="tt" :class="num==1?'on':''" @click="changeNum('1')">财务咨询</view>
			<view class="tt" :class="num==2?'on':''" @click="changeNum('2')">税务咨询</view>
			<view class="tt" :class="num==3?'on':''" @click="changeNum('3')">法律咨询</view>
		</view>
		<view class="pdtb20"></view>
		
		<view class="mglr4 myLoanList fs13 mgt15" v-show="num==1">
			<view class="item" v-for="(item,index) in loanData" :key="index">
				<view class="oneLine flexRowBetween">
					<view class="">咨询时间：2020.01.15</view>
					<view class="color6 flexEnd" @click="alertShow"><image class="delIcon" src="../../static/images/my-advice-icon.png" mode=""></image>删除</view>
				</view>
				<view class="pdlr4 mgt10">复活甲考试的老汉给就过来开开发德生科技咖喱咖啡都是国家首付款了感觉粉色考虑的加工费但是看了就过来开发多久钢结构浪费的时间里</view>
			</view>
		</view>
		<view class="mglr4 myLoanList fs13 mgt15" v-show="num==2">
			<view class="item" v-for="(item,index) in loanData" :key="index">
				<view class="oneLine flexRowBetween">
					<view class="">咨询时间：2020.01.15</view>
					<view class="color6 flexEnd" @click="alertShow"><image class="delIcon" src="../../static/images/my-advice-icon.png" mode=""></image>删除</view>
				</view>
				<view class="pdlr4 mgt10">复活甲考试的老汉给就过来开开发德生科技咖喱咖啡都是国家首付款了感觉粉色考虑的加工费但是看了就过来开发多久钢结构浪费的时间里</view>
			</view>
		</view>
		<view class="mglr4 myLoanList fs13 mgt15" v-show="num==3">
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
				num:1
			}
		},
		onLoad() {
			const self = this;
			// self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			changeNum(num){
				const self=this;
				if(num!=self.num){
					self.num = num
				}
			},
			alertShow(){
				const self=this;
				self.is_alertShow = !self.is_alertShow;
				self.is_show = !self.is_show;
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
	@import "../../assets/style/orderNav.css";
	@import "../../assets/style/myOrder.css";
	page{background: #F5F5F5;padding-bottom:60px;}
	
</style>
