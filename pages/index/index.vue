<template>
	<view>
		<u-tabs style="position: fixed; width: 100%; z-index: 99;" :list="list" :is-scroll="false" :current="current" @change="change"
		 bg-color="#f1f1f1"></u-tabs>
		<u-top-tips ref="uTips"></u-top-tips>
		<view class="list-content">
			<view class="file" v-for="item in dirList" v-if="selectType=='all'" :key="item.name" @click="clickFile(item.Prefix,'directory')">
				<image :src="iconList.directory" mode=""></image>
				<view class="file-name">
					{{item.Prefix}}
				</view>
			</view>
			<view class="file" v-for="item in fileList" v-if="selectType==item.type||selectType=='all'" :key="item.name" @click="clickFile(item.Key,item.type)">
				<image :src="iconList[item.type]" mode=""></image>
				<view class="file-name">
					{{item.Key}}
				</view>
			</view>
		</view>
		<tabbar></tabbar>
	</view>
</template>

<script>
	import {
		url
	} from "../conf.js"

	export default {
		globalData: {},
		data() {
			return {
				list: [{
					name: '全部'
				}, {
					name: '视频'
				}, {
					name: '图片'
				}, {
					name: '文档'
				}, {
					name: '其他'
				}],
				current: 0,
				dirList: [1, 2, 3],
				selectType: "all",
				fileList: [],
				iconList: {
					directory: "../../static/icon/file.png",
					video: "../../static/icon/video-icon.png",
					picture: "../../static/icon/picture-icon.png",
					document: "../../static/icon/document-icon.png",
					other: "../../static/icon/other-icon.png"
				}
			}
		},

		onLoad(options) {
			// uni.setNavigationBarTitle({
			// 	title:'haha'
			// });
			this.getObjectLsit()
			var webView = this.$mp.page.$getAppWebview();
			webView.setStyle({
				titleNView: {
					autoBackButton: false
				}
			})
		},
		methods: {
			change(index) {
				const typeArr = ["all", "video", "picture", "document", "other"]
				this.current = index;
				this.selectType = typeArr[index]
			},
			clickFile(key, type) {
				switch (type) {
					case "directory":
						this.getObjectLsit(key)
						break;
					case "video":
						uni.request({
							url: url + "/getObjectUrl",
							data: {
								key
							},
							method: "POST",
							dataType: "json",
							success: (result) => {
								let url = encodeURIComponent(result.data.Url)
								console.log(url)
								uni.redirectTo({
									url: `../detail/detail?url=${url}&type=${type}`,
									animationType: "zoom-fade-out"
								})
							},
							fail: (err) => {
								this.$refs.uTips.show({
									title: "获取文件信息失败，详情联系管理员(虽然管理员不一定理你)",
									type: 'error',
									duration: '2300'
								})
								console.log(err)
							}
						})
						break;
				}
			},
			getObjectLsit(path) {
				uni.request({
					url: url + "/getObjectLsit",
					data: {
						path
					},
					method: "GET",
					dataType: "json",
					success: (result) => {
						if (!path) {
							this.dirList = result.data.CommonPrefixes
							this.fileList = result.data.Contents
						} else {
							console.log(path)
							uni.navigateTo({
								url: "../directory/directory?path=" + path,
								animationType: "zoom-fade-out"
							})
						}
						console.log(result)
					},
					fail: (err) => {
						this.$refs.uTips.show({
							title: "获取网盘数据失败，详情联系管理员(虽然管理员不一定理你)",
							type: 'error',
							duration: '2300'
						})
						console.log(err)
					}
				})
			}
		}
	}
</script>

<style lang="scss">
	.list-content {
		padding: 12rpx;
		display: flex;
		justify-content: space-around;
		align-items: center;
		flex-wrap: wrap;
		padding-top: 90rpx;

		.file {
			width: 200rpx;
			height: 200rpx;
			margin: 20rpx;
			border: 1rpx solid rgba($color: #333333, $alpha: 0.3);
			border-radius: 10rpx;
			position: relative;
			display: flex;
			flex-direction: column;
			justify-content: center;
			align-items: center;

			image {
				width: 110rpx;
				height: 110rpx;
			}


			.file-name {
				margin-top: 10rpx;
				font-size: 20rpx;
				color: #3d3d3d;
				width: 100%;
				overflow: hidden;
				text-overflow: ellipsis;
				white-space: nowrap;
				text-align: center;
				padding: 0 15rpx;
			}
		}

	}

	.list-content::after {
		content: " ";
		flex: auto;
	}
</style>
