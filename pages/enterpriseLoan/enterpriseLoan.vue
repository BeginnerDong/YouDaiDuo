<template>
	<view>
		
		<view class="pdlr4">
			<view class="loanList pdt15 center">
				<view class="item" v-for="(item,index) in loadData" :key="index"  @click="Router.navigateTo({route:{path:'/pages/enterpriseDetail/enterpriseDetail'}})">
					<image class="pic" src="../../static/images/the-loan-img.png" mode=""></image>
					<view class="tit">{{item.title}}</view>
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
				is_show:false,
				loadData:[{title:'商业贷款'},{title:'政策性贷款'}]
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
	.loanList .item{width: 100%;height: 460rpx;margin-bottom: 30rpx;overflow: hidden;position: relative;}
	.loanList .item .pic{width: 100%;height: 100%;display: block;}
	.loanList .item .tit{position: absolute;bottom: 0;left: 0;right: 0;padding: 0 4%;box-sizing: border-box;width: 100%;height: 85rpx;line-height: 85rpx;background: rgba(0,0,0,0.5); color: #fff;}
</style>
