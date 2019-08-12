<template>
	<view class="">
		<!-- 头部宣传 -->
		<view class="head uni-flex uni-column">
			<view class="head-item" style="font-size: 40upx;">
				AI体验中心
			</view>
			<view class="">
				马上体验黑科技!
			</view>
			<view class="head-item" style="border-radius: 30upx;border: 1px solid white; width: 200upx;text-align: center;" @click="call(phone)">
				技术咨询
			</view>
		</view>
		<!-- AI能力列表 -->
		<view class="uni-flex uni-center" style="width: 100%;flex-wrap: wrap;">
			<view class="ailist" v-for="(item,index) in word" :key='index' @click="go(index)">
				{{item}}
			</view>
		</view>
		<!-- 客服电话 -->
		<view class="foot">
			<view class="foot-item">
			更多AI能力，可二次开发	
			</view>
			<view class="foot-item" @click="call(phone)">
				客服电话：<text class="uni-link">{{phone}}</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				word: ['通用文字识别', '身份证识别', '银行卡识别', '车牌识别', '驾驶证识别', '行驶证识别', '营业执照识别', '增值税发票', '出租车票识别', '火车票识别', '手写识别', '定额发票识别','通用机打发票','机动车销售发票','图像主题检测','植物识别','动物识别','菜品识别','车型识别','地标识别','红酒识别','货币识别','图像审核'],
				phone:'010-86466630'
			}
		},
		onLoad() {

		},
		onShareAppMessage() {
			return{
				title:'明志AI邀您体验黑科技',
				path:'/pages/index/index'
			}
		},
		methods: {
			go(index){
				uni.navigateTo({
					url:'../basic/basic'
				})
			},
			call(e){
				uni.makePhoneCall({
					phoneNumber:e
				})
			}
		}
	}
</script>

<style>
	.head {
		background-color: #13227a;
		color: #FFFFFF;
		width: 100%;
		height: 300upx;
		padding: 10upx 100upx;
		justify-content: space-around;
	}

	.ailist {
		margin-left: 30upx;
		margin-top: 20upx;
		height: 80upx;
		line-height: 80upx;
		width: 330upx;
		border: 1upx solid #BEBEBE;
	}

	.foot {
		display: flex;
		flex-direction: column;
		width: 100%;
		justify-content: center;
		align-content: center;
		text-align: center;
	}

	.foot-item{
		
		color: gray;
	}
</style>
