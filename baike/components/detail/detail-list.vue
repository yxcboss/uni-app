<template>
	<view class="common-list u-f">
		<view class="common-list-l">
			<image :src="item.userpic" mode="widthFix" lazy-load></image>
		</view>
		<view class="common-list-r">
			<view class="u-f-ac u-f-jsb">
				<view class="u-f-ac">
					{{item.username}}
					<!-- <view class="tag-sex icon iconfont" :class="item.sex == 0 ? 'icon-nan':'icon-nv'">{{item.age}}</view> -->
					<TagSexAge :age="item.age" :sex="item.sex"></TagSexAge>
				</view>
				<view class="icon iconfont icon-zengjia" v-show="!isguanzhu" @tap="guanzhu">关注</view>
			</view>
			<view class="time">
				26天前
			</view>
			<view>{{item.title}}</view>
			<view class="u-f-ajc" style="flex-direction: column;">
				<!-- 图片 -->
				<block v-for="(pic,index) in item.morepic">
					<image :src="pic" 
					mode="widthFix" 
					style="margin-bottom: 20upx;" 
					lazy-load
					@tap="imgdetail(index)"></image>
				</block>
				<!-- 视频 -->
				<template v-if="item.video">
					<view class="common-list-play icon iconfont icon-bofang"></view>
					<view class="common-list-playinfo">
						{{item.video.looknum}} 次播放 {{item.video.long}}
					</view>
				</template>

				<!-- 分享 -->
				<view v-if="item.share" class="common-list-share u-f-ac">
					<image src="../../static/demo/datapic/14.jpg" mode="widthFix" lazy-load></image>
					<view>{{item.share.title}}</view>
				</view>
			</view>
			<view class="u-f-ac u-f-jsb">
				<view>{{item.path}}</view>
				<view class="u-f-ac">
					<view class="icon iconfont icon-zhuanfa">{{item.sharenum}}</view>
					<view class="icon iconfont icon-pinglun1">{{item.commentnum}}</view>
					<view class="icon iconfont icon-dianzan1">{{item.goodnum}}</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import TagSexAge from "../../components/common/tag-sex-age.vue";
	export default {
		components:{
			TagSexAge
		},
		props: {
			item: Object,
			index: Number
		},
		data() {
			return {
				isguanzhu: this.item.isguanzhu
			};
		},
		methods: {
			guanzhu() {
				this.isguanzhu = true;
				uni.showToast({
					title: '关注成功',
				});
			},
			imgdetail(index){
				uni.previewImage({
					current: index,
				    urls: this.item.morepic,
				    indicator:"number"
				});
			}
		}
	}
</script>

<style scoped>
	.common-list {
		/* padding: 20upx; */
	}

	.common-list-l {
		flex-shrink: 0;
	}

	.common-list-l image {
		width: 60upx;
		height: 60upx;
		border-radius: 100%;
	}

	.common-list-r {
		flex: 1;
		margin-left: 15upx;
		border-bottom: 1upx solid #EEEEEE;
		padding-bottom: 10upx;
	}

	.common-list-r>view:nth-child(3)>image {
		/* width: 100%; */
		border-radius: 10upx;
	}

	.common-list-r>view:nth-child(1)>view:first-child {
		color: #999999;
		font-size: 32upx;
	}

	.tag-sex {
		background: #007AFF;
		color: #FFFFFF;
		font-size: 23upx;
		padding: 5upx 10upx;
		margin-left: 10upx;
		border-radius: 20upx;
		line-height: 22upx;
	}

	.common-list-r>view:nth-child(1)>view:last-child {
		background: #EEEEEE;
		padding: 0 10upx;
		font-size: 26upx;
	}

	.common-list-r>view:nth-child(2) {
		font-size: 32upx;
		padding: 12upx 0;
	}

	.common-list-r>view:nth-child(3) {
		position: relative;
	}

	.common-list-play,
	.common-list-playinfo {
		position: absolute;
		color: #FFFFFF;
	}

	.common-list-play {
		font-size: 130upx;
	}

	.common-list-playinfo {
		right: 10upx;
		bottom: 10upx;
		background: rgba(51, 51, 51, 0.73);
		border-radius: 20upx;
		padding: 0 20upx;
		font-size: 26upx;
	}

	.common-list-r>view:nth-child(4)>view {
		color: #AAAAAA;
	}

	.common-list-r>view:nth-child(4)>view:nth-child(2)>view {
		margin-left: 10upx;
		padding-left: 5upx;
	}

	.common-list-share {
		background: #EEEEEE;
		width: 100%;
		padding: 10upx;
		border-radius: 10upx;
	}

	.common-list-share>image {
		width: 200upx;
		height: 150upx;
		margin-right: 10upx;
	}
	
	.common-list-r{
		border-bottom: 0;
	}
	.common-list{
		border-bottom: 1upx solid #EEEEEE;
	}
	.common-list-r-time{
		padding: 15upx 0;
		color: #CCCCCC!important;
		font-size: 25upx;
		background: #FFFFFF!important;
	}
	.common-list-r>view:nth-child(1)>view:nth-child(1)>view:first-child{
		color: #999999;
		font-size: 32upx;
	}
	
	.common-list-r>view:nth-child(1)>view:nth-child(1)>view:last-child{
		background: #EEEEEE;
		padding: 0 10upx;
		font-size: 26upx;
	}
</style>
