<template>
	<view>
		<view class="mglr4 myRowBetween">
			<view class="item flexRowBetween" v-show="sliderData.url&&sliderData.url!='1'" >
				<view class="ll">资金需求(万元)</view>
				<view class="rr">
					<input type="number" v-model="submitData.keywords" placeholder="请输入" placeholder-class="placeholder" />
				</view>
			</view>
			<view class="item flexRowBetween">
				<view class="ll">联系人</view>
				<view class="rr">
					<input type="text" v-model="submitData.title" placeholder="请输入" placeholder-class="placeholder" />
				</view>
			</view>
			<view class="item flexRowBetween">
				<view class="ll">联系电话</view>
				<view class="rr">
					<input type="text" v-model="submitData.phone" placeholder="请输入" placeholder-class="placeholder" maxlength='11'/>
				</view>
			</view>
			
		</view>
		<view class="submitbtn" style="margin-top: 200rpx;">
			<button class="btn" type="button" open-type="getUserInfo" @getuserinfo="Utils.stopMultiClick(submit)">提交</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				Utils:this.$Utils,
				submitData:{
					type:1,
					title:'',
					phone:'',
					keywords:'',
					relation_id:'',
					behavior:''
				},
				sliderData:{}
			}
		},
		
		onLoad(options) {
			const self = this;
			self.submitData.relation_id = options.id;
			self.submitData.behavior = options.behavior;
			// self.$Utils.loadAll(['getMainData'], self);
			self.$Utils.loadAll(['getSliderData'], self);
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
			
			submit() {
				const self = this;
				uni.setStorageSync('canClick', false);
				uni.showLoading({
					title: '提交中...',
					mask: true
				});
				const pass = self.$Utils.checkComplete(self.submitData);
				console.log('pass', pass);
				console.log('self.submitData',self.submitData)
				
				if (pass) {	
					const callback = (user, res) => {
						console.log(res)
						self.messageAdd();
					};
					self.$Utils.getAuthSetting(callback);
				
				} else {
					uni.setStorageSync('canClick', true);
					self.$Utils.showToast('请补全信息', 'none')
				};
			},
			
			messageAdd() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				if(!wx.getStorageSync('user_info')||!wx.getStorageSync('user_info').headImgUrl){
				  postData.refreshToken = true;
				};
				postData.data = {};
				postData.data = self.$Utils.cloneForm(self.submitData);
				const callback = (data) => {				
					if (data.solely_code == 100000) {					
						self.$Utils.showToast('提交成功', 'none', 1000)
						setTimeout(function() {
							uni.navigateBack({
								delta:1
							})
						}, 1000);
						
					} else {
						uni.setStorageSync('canClick', true);
						self.$Utils.showToast(data.msg, 'none', 1000)
					}	
				};
				self.$apis.messageAdd(postData, callback);
			},
			
		}
	};
</script>

<style>
	@import "../../assets/style/editInfor.css";
	page{padding-bottom: 60px;}
</style>
