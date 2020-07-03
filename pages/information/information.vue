<template>
	<view>
		<view class="mglr4 flexRowBetween newsList pdtb15">
			<view class="item" v-for="(item,index) in mainData" :key="index" :data-id="item.id"
			@click="Router.navigateTo({route:{path:'/pages/informationDetail/informationDetail?id='+$event.currentTarget.dataset.id}})">
				<view class="pic">
					<image :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''" mode=""></image>
				</view>
				<view class="tit avoidOverflow pdtb5">{{item.title}}</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				mainData:[]
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
					
						uni.setNavigationBarTitle({
						    title: self.sliderData.url==1?'资讯':'贷款资讯'
						});
					}
					self.$Utils.finishFunc('getSliderData');
				};
				self.$apis.labelGet(postData, callback);
			},
			
			getMainData() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					thirdapp_id:2
				};
				postData.paginate = self.$Utils.cloneForm(self.paginate);
				postData.getBefore = {
					article:{
						tableName:'Label',
						middleKey:'menu_id',
						key:'id',
						searchItem:{
							title: ['in', ['贷款资讯']],
						},
						condition:'in'
					}
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData,res.info.data)
					}
					console.log(self.mainData)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.articleGet(postData, callback);
			},
			
		}
	};
</script>

<style>
	.newsList{flex-wrap: wrap;align-items: flex-start;}
	.newsList .item{width: 330rpx;margin-bottom: 30rpx;}
	.newsList .item .pic{width: 100%;height: 240rpx;}
	.newsList .item .pic image{width: 100%;height:100%; display: block;}
</style>
