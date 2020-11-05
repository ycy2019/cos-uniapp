<template>
	<view>
		<view id="user-content">
			<input type="text" id="user-input" placeholder="请输入用户名" />
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {

			};
		}
	}
</script>

<style lang="scss">
	#user-content {
		width: 536upx;
		height: 78upx;
		background-image: url(../../static/image/user.png);
		background-repeat: no-repeat;
		background-size: cover;
		padding-left: 120upx;

		input {
			height: 100%;
			
		}
	}
</style>
