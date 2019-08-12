<template>
	<view>
		<view class="imageBox">
			<image :src="imageSrc" mode="aspectFit" style="width: 650upx;height: 400upx;"></image>
		</view>
		<view class="uni-padding-wrap">
			<view class="wordlist" v-for="(item,index) in words" :key='index'>
				<view class="uni-center" style="width: 30%;">
					{{index+1}}
				</view>
				<view class="uni-flex-item" style="color: #13227A;">
					{{item.words}}
				</view>


			</view>
		</view>
		<!-- button -->
		<view class="uni-padding-wrap uni-common-mt">
			<button type="" @click="chooseImage">上传图片</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				words: [],
				imageSrc: ''
			};
		},
		onShareAppMessage() {
			return {
				title: '明志AI邀您体验黑科技',
				path: '/pages/index/index'
			}
		},
		methods: {
			chooseImage: function() {
				uni.chooseImage({
					count: 1,
					sizeType: ['compressed'],
					sourceType: ['album'],
					success: (res) => {
						console.log('chooseImage success, temp path is', res.tempFilePaths[0])
						var imageSrc = res.tempFilePaths[0]
						uni.uploadFile({
							url: 'https://promotion.mzsat.cn/api/baidu/basic',
							filePath: imageSrc,
							fileType: 'image',
							name: 'file',
							success: (res) => {
								console.log('uploadImage success, res is:', res.data)
								console.log(typeof(res.data))
								uni.showToast({
									title: '上传成功',
									icon: 'success',
									duration: 1000
								})
								this.imageSrc = imageSrc;
								var data = JSON.parse(res.data)
								this.words = data.words_result

							},
							fail: (err) => {
								console.log('uploadImage fail', err);
								uni.showModal({
									content: err.errMsg,
									showCancel: false
								});
							}
						});
					},
					fail: (err) => {
						console.log('chooseImage fail', err)
					}
				})
			}
		}
	}
</script>

<style>
	.imageBox {
		width: 100%;
		height: 500upx;
		background-color: #666666;
		justify-content: center;
		align-content: center;
		display: flex;
	}

	.wordlist {
		border: 1upx solid #999999;
		width: 100%;
		height: 80upx;
		line-height: 80upx;
		display: flex;
		flex-direction: row;
		margin-top: 30upx;
		align-items: center;
	}

	button {
		background-color: #13227A;
		color: #FFFFFF;
	}
</style>
