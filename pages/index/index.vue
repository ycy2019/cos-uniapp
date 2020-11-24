<template>
	<view>
		<u-tabs :list="list" :is-scroll="false" :current="current" @change="change" bg-color="#f1f1f1"></u-tabs>
		<view class="list-content">
			<view class="file" v-for="item in list" :key="item.name">
				<image src="../../static/icon/file.png" mode=""></image>
			</view>
		</view>
		<tabbar></tabbar>
	</view>
</template>

<script>
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
				current: 0
			}
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
			justify-content: center;
			align-items: center;
			
			image{
				width: 120rpx;
				height: 120rpx;
			}
		}
		
	}

	.list-content::after {
		content: " ";
		flex: auto;
	}
</style>
