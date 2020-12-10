<template>
	<view style="width: 100%;">
		<video id="myVideo" :src="videoPath" controls autoplay enable-play-gesture=true style="width: 100%;"
		 @fullscreenchange="fullscreenchange($event)"></video>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				videoPath: ""
			};
		},
		onReady() {
			// 获取 video 上下文 videoContext 对象
			this.videoContext = uni.createVideoContext('myVideo');
			// 进入全屏状态
			this.videoContext.requestFullScreen();
		},
		onLoad(option) {
			console.log(option)
			let type = option.type
			switch (type) {
				case "video":
					this.videoPath = option.url
					break;
			}
		},
		methods: {
			fullscreenchange(event) {
				if (!event.detail.fullScreen) {
					uni.navigateBack({});
				}
			}
		}
	}
</script>

<style lang="scss">

</style>
