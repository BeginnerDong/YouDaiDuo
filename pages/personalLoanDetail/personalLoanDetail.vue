<template>
	<view>
		
		<view class="detailxqBan">
			<image :src="mainData.bannerImg&&mainData.bannerImg[0]?mainData.bannerImg[0].url:''" mode=""></image>
		</view>
		<view class="mglr4 pdtb15">{{mainData.title}}</view>
		<view class="f5H10"></view>
		<view class="mglr4 pdtb15">
			<view class="ftw fs15 pdb10">详情描述</view>
			<view class="xqInfor">
				<view class="cont fs12">
					<view class="content ql-editor" style="padding:0;"
					v-html="mainData.content">
					</view>
				</view>
			</view>
			
		</view>
		<view class="submitbtn pdt30 pdb20">
			<button class="btn" type="button" 
			@click="Router.navigateTo({route:{path:'/pages/personalConsult/personalConsult?id='+mainData.id+'&behavior=1'}})">立即咨询</button>
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
		
		onLoad(options) {
			const self = this;
			self.id = options.id;
			self.$Utils.loadAll(['getMainData'], self);
		},
		
		methods: {
			
			getMainData(){
			    var self = this;
			    var postData = {};
			    postData.searchItem = {
					menu_id:self.id,
					thirdapp_id:2,
				};
			    var callback = function(res){
			        if(res.info.data.length>0&&res.info.data[0]){
						self.mainData  =res.info.data[0];
						const regex = new RegExp('<img', 'gi');
						self.mainData.content = self.mainData.content.replace(regex, `<img style="max-width: 100%;"`);
			        };    
					self.$Utils.finishFunc('getMainData');
			    };
				self.$apis.articleGet(postData, callback);
			},
		}
	};
</script>

<style>
	@import "../../assets/style/detial.css";
</style>
