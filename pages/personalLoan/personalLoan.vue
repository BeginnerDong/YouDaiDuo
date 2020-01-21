<template>
	<view>
		
		<view class="pdlr4">
			<view class="loanList pdt15 center">
				<view class="item" v-for="(item,index) in mainData" :key="index"  :data-id="item.id"
				@click="Router.navigateTo({route:{path:'/pages/personalLoanDetail/personalLoanDetail?id='+$event.currentTarget.dataset.id}})">
					<image class="pic" :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''" mode=""></image>
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
				mainData:[],
				loadData:[{title:'个人消费贷款'},{title:'个人经营贷款'}]
			}
		},
		
		onLoad() {
			const self = this;
			self.$Utils.loadAll(['getMainData'], self);
		},
		
		methods: {
			
			
			getMainData(){
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
							title:['in',['个人贷款']]
						},
						condition:'in',
					}
				};
				postData.order = {
					listorder:'desc'
				};
			    var callback = function(res){
			        if(res.info.data.length>0&&res.info.data[0]){
						self.mainData.push.apply(self.mainData,res.info.data)
			        };    
					self.$Utils.finishFunc('getMainData');
			    };
				self.$apis.labelGet(postData, callback);
			},
		}
	};
</script>

<style>
	.loanList .item{width: 100%;height: 460rpx;margin-bottom: 30rpx;overflow: hidden;position: relative;}
	.loanList .item .pic{width: 100%;height: 100%;display: block;}
	.loanList .item .tit{position: absolute;bottom: 0;left: 0;right: 0;padding: 0 4%;box-sizing: border-box;width: 100%;height: 85rpx;line-height: 85rpx;background: rgba(0,0,0,0.5); color: #fff;}
</style>
