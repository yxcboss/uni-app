<template>
	<view>
		搜索页
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
				
			}
		},
		//监听原生标题栏点击事件
		onNavigationBarButtonTap(e){
			console.log(e)
			if(!e.index){
				uni.navigateBack({
				    delta: 1
				});
			}
		},
		// 监听原生标题栏搜索输入框输入内容变化事件
		onNavigationBarSearchInputChanged(e){
			console.log(e)
		},
		// 监听原生标题栏搜索输入框搜索事件
		onNavigationBarSearchInputConfirmed(e){
			console.log(e)
		},
		methods: {
			
		}
	}
</script>

<style>

</style>
