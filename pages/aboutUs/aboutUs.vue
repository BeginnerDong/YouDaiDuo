<template>
	<view>
		
		<view class="detailxqBan" style="height: 400rpx;">
			<image src="../../static/images/about-us-img.png" mode=""></image>
		</view>
		<view class="mglr4 adrsLis">
			<view class="item borderB1">
				<image class="icon" src="../../static/images/about-us-icon2.png" mode=""></image>
				<view>{{mainData.title}}</view>
			</view>
			<view class="item">
				<image class="icon" src="../../static/images/about-us-icon1.png" mode=""></image>
				
				<view>{{mainData.description}}</view>
			</view>
		</view>
		<view class="f5H10"></view>
		<view class="mglr4 pdtb15">
			<view class="ftw fs15 pdb10">关于我们</view>
			<view class="xqInfor">
				<view class="cont fs13">
					<view class="content ql-editor" style="padding:0;"
					v-html="mainData.content">
					</view>
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
				mainData:{}
			}
		},
		
		onLoad() {
			const self = this;
			self.$Utils.loadAll(['getMainData'], self);
		},
		
		methods: {
			
			getMainData() {
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
						self.mainData = res.info.data[0];
						const regex = new RegExp('<img', 'gi');
						self.mainData.content = self.mainData.content.replace(regex, `<img style="max-width: 100%;"`);
					};
					console.log(self.mainData)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.articleGet(postData, callback);
			},
		}
	};
</script>

<style>
	@import "../../assets/style/detial.css";
	.adrsLis .item{padding: 30rpx 0;align-items: flex-start;padding-left: 50rpx;position: relative;}
	.adrsLis .item .icon{width: 36rpx;height: 36rpx; display: block;position: absolute;top: 30rpx;left: 0;}
	.xqInfor{line-height: 44rpx;}
</style>
