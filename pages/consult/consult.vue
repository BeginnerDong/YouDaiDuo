<template>
	<view>
		
		<view class="pdtb5 item">
			<textarea v-model="submitData.description" placeholder="请输入问题" placeholder-class="placeholder" />
		</view>
		<view class="f5H5"></view>
		<view class="mglr4 myRowBetween">
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
					type:2,
					title:'',
					phone:'',
					description:'',
					relation_id:''
				}
			}
		},
		
		onLoad(options) {
			const self = this;
			self.submitData.relation_id = options.id;
			//self.submitData.behavior = options.behavior;
			// self.$Utils.loadAll(['getMainData'], self);
		},
		
		methods: {
			
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
	.myRowBetween .item textarea{padding: 0;border: none;}
</style>
