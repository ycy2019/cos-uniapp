<template>
	<view>
		<view>
			<view class="u-page">
				<!-- 所有内容的容器 -->
			</view>
			<!-- 与包裹页面所有内容的元素u-page同级，且在它的下方 -->
			<u-tabbar v-model="current" :list="list" :mid-button="true"></u-tabbar>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list: [{
						iconPath: "/static/tababr/page.png",
						selectedIconPath: "home-fill",
						text: '资源',
						isDot: true,
						customIcon: false,
					},
					{
						iconPath: "https://cdn.uviewui.com/uview/common/min_button.png",
						selectedIconPath: "https://cdn.uviewui.com/uview/common/min_button_select.png",
						text: '上传',
						midButton: true,
						customIcon: false,
					},
					{
						iconPath: "account",
						selectedIconPath: "account-fill",
						text: '我的',
						isDot: false,
						customIcon: false,
					},
				],
				current: 0
			}
		},
	}
</script>

<style lang="scss">

</style>
