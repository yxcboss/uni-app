<template>
	<view class="home-info u-f-ac" @tap="openuserspace">
		<view class="left u-f-ac">
			<image :src="homeinfo.userpic" mode="widthFix" lazy-load></image>
			<view class="u-f1">
				<view>{{homeinfo.username}}</view>
				<view>总访客 {{homeinfo.totalnum}}  今日 {{homeinfo.todaynum}}</view>
			</view>
		</view>
		<view class="icon iconfont icon-jinru"></view>
	</view>
</template>

<script>
	export default {
		props:{
			homeinfo:Object
		},
		methods:{
			openuserspace(){
				uni.navigateTo({
					url: '../../pages/user-space/user-space',
					success: res => {},
					fail: () => {},
					complete: () => {}
				});
			}
		}
	}
</script>

<style scoped>
.home-info{
	padding: 20upx 40upx;
	justify-content: space-between;
}
.home-info>.left>image{
	flex-shrink: 0;
	width: 100upx;
	height: 100upx;
	border-radius: 100%;
	margin-right: 15upx;
}
.home-info>view:first-of-type>view:first-child{
	font-size: 32upx;
}
.home-info>view:first-of-type>view:last-child{
	color: #BBBBBB;
}
.home-info>view:last-of-type{
	height: 100%;
}

</style>
