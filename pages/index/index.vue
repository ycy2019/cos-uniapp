<template>
	<view>
		<u-tabs :list="list" :is-scroll="false" :current="current" @change="change" bg-color="#f1f1f1"></u-tabs>
		
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

</style>
