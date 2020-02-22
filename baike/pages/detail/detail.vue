<template>
	<view>
		<detailList :item="detail"></detailList>
		
		<view class="u-comment-title">最新评论 {{comment.count}}</view>
		<view class="uni-comment u-comment">
			<block v-for="(item,index) in comment.list" :key="index">
				<commentList :item="item" :index="index"></commentList>
			</block>
		</view>
		<view style="height: 120upx;"></view>
		<!-- 输入框 -->
		<user-chat-bottom @submit="submit"></user-chat-bottom>
		
		<moreShare :isshow='shareshow' @togle="togle"></moreShare>
	</view>
</template>

<script>
	import detailList from '../../components/detail/detail-list.vue';
	import time from "../../common/time.js";
	import commentList from "../../components/detail/comment-list.vue";
	import userChatBottom from '../../components/user-chat/user-chat-bottom.vue';
	import moreShare from "../../components/common/more-share.vue"
	export default {
		components: {
			detailList,
			commentList,
			userChatBottom,
			moreShare
		},
		data() {
			return {
				shareshow:false,
				comment:{
					count:20,
					list:[]
				},
				detail: {
					userpic: "../../static/demo/userpic/12.jpg",
					username: "哈哈",
					sex: 0, //0 男 1 女
					age: 25,
					isguanzhu: false,
					title: "我是标题",
					titlepic: "../../static/demo/datapic/13.jpg",
					morepic: ["../../static/demo/datapic/13.jpg", "../../static/demo/datapic/14.jpg",
						"../../static/demo/datapic/15.jpg"
					],
					video: false,
					share: false,
					path: "深圳 龙岗",
					sharenum: 20,
					commentnum: 30,
					goodnum: 20
				},
			}
		},
		onLoad(e) {
			this.initdata(JSON.parse(e.detailData));
			this.getcomment();
		},
		// 监听导航右边按钮
		onNavigationBarButtonTap(e) {
			if(e.index==0){
				this.togle();
			}
		},
		methods: {
			togle(){
				this.shareshow = !this.shareshow;
			},
			initdata(val) {
				uni.setNavigationBarTitle({
					title: val.title
				});
			},
			getcomment(){
				let arr=[
					// 一级评论
					{
						id:1,
						fid:0,
						userpic:"https://img-cdn-qiniu.dcloud.net.cn/uniapp/images/uni@2x.png",
						username:"小猫咪",
						time:"1555400035",
						data:"支持国产，支持DCloud!",
					},
					// 子级评论
					{
						id:2,
						fid:1,
						userpic:"https://img-cdn-qiniu.dcloud.net.cn/uniapp/images/uni@2x.png",
						username:"小猫咪",
						time:"1555400035",
						data:"支持国产，支持DCloud!",
					},
					{
						id:3,
						fid:1,
						userpic:"https://img-cdn-qiniu.dcloud.net.cn/uniapp/images/uni@2x.png",
						username:"小猫咪",
						time:"1555400035",
						data:"支持国产，支持DCloud!",
					},
					{
						id:4,
						fid:0,
						userpic:"https://img-cdn-qiniu.dcloud.net.cn/uniapp/images/uni@2x.png",
						username:"小猫咪",
						time:"1555400035",
						data:"支持国产，支持DCloud!",
					},
				];
				for (let i = 0; i < arr.length; i++) {
					arr[i].time=time.gettime.gettime(arr[i].time);
				}
				this.comment.list=arr;
			},
			submit(data){
				let obj={
					id:1,
					fid:0,
					userpic:"https://img-cdn-qiniu.dcloud.net.cn/uniapp/images/uni@2x.png",
					username:"小猫咪",
					time:time.gettime.gettime(new Date().getTime()),
					data:data,
				};
				this.comment.list.push(obj);
			},
		}
	}
</script>

<style>
.u-comment{
	padding: 0 20upx;
}
.u-comment-title{
	padding: 20upx;
	font-size: 30upx;
	font-weight: bold;
}
</style>
