<template>
	<view>
		<u-tabs :list="list" :is-scroll="false" :current="current" @change="change" bg-color="#f1f1f1"></u-tabs>
		<view class="list-content">
			<view class="file" v-for="item in dirList" :key="item.name">
				<image :src="iconList.directory" mode=""></image>
				<view class="file-name">
					{{item.Prefix}}
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
	console.log(url)
	export default {
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
				dirList: [],
				iconList: {
					directory: "../../static/icon/file.png",
					video: "../../static/icon/video-icon.png",
					picture: "../../static/icon/picture-icon.png",
					document: "../../static/icon/document-icon.png",
					other: ""
				}
			}
		},

		onLoad() {
			uni.request({
				url: url + "/getObjectLsit",
				method: "GET",
				dataType: "json",
				success: (result) => {
					this.dirList = result.data.CommonPrefixes
					console.log(result)
				},
				fail: function(err) {
					alert("获取网盘数据失败，详情联系管理员")
					console.log(err)
				}
			})
		},
		methods: {
			change(index) {
				this.current = index;
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
				font-size: 16rpx;
				color: #3d3d3d;
			}
		}

	}

	.list-content::after {
		content: " ";
		flex: auto;
	}
</style>
