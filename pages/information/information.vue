<template>
	<view>
		<view class="mglr4 flexRowBetween newsList pdtb15">
			<view class="item" v-for="(item,index) in newsData" :key="index" @click="Router.navigateTo({route:{path:'/pages/informationDetail/informationDetail'}})">
				<view class="pic"><image src="../../static/images/information-img.png" mode=""></image></view>
				<view class="tit avoidOverflow pdtb5">闪贷贷款借贷网资讯为您提供最新的贷款新闻</view>
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
				newsData:[{},{},{},{},{},{},{},{}]
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
	.newsList{flex-wrap: wrap;align-items: flex-start;}
	.newsList .item{width: 330rpx;margin-bottom: 30rpx;}
	.newsList .item .pic{width: 100%;height: 240rpx;}
	.newsList .item .pic image{width: 100%;height:100%; display: block;}
</style>
