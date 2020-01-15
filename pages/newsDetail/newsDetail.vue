<template>
	<view>
		
		<view class="pdlr4">
			<view class="pdt15 pdb10 center">夫妻因婚外情离婚，无过错方可以向对方要多少精神损害赔偿?夫妻因婚外情离婚夫妻因婚外情离婚</view>
			<view class="flexEnd fs12 color9 pdb15">2020-01-15</view>
			<view class="xqInfor">
				<view class="cont fs12">
					<view>管理客服电话还房贷两个号和个梵蒂冈悲愤交加鹤骨鸡肤供货方点击可供货方都拉黑干活的放假开个会过分的话看风格算旷工海景房大咖苏广号放假开始估还热供货方大咖苏广会热</view>
					<view>花港饭店两三个号换个卡富家大室联合国利干活附近的开个会发和公交卡方大化工干活附近的看和回访电话收购房款好几个红烧豆腐及控股</view>
					<view>就发过来的手机关机刚认识的就过来九分的考虑过佛光更进反馈的和过分的话公司交开个会干活附近的看和国防科大换个飞机看低功耗非结构化供货方健康的供货方看到</view>
					<view><image src="../../static/images/details-img.png" mode="widthFix"></image></view>
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
				is_show:false
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
	@import "../../assets/style/detial.css";
	page{padding-bottom: 60rpx;}
</style>
