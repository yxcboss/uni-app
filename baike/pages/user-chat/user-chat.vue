<template>
	<view>
		<scroll-view id="scrollview" scroll-y :scroll-top="scrollTop"
		:scroll-with-animation="true"
		:style="{height:style.contentH+'px'}">
			
			<!-- 聊天列表 -->
			<block v-for="(item,index) in list" :key="index">
				<userChatList :item="item" :index="index"></userChatList>
			</block>
			
		</scroll-view>
		
		<!-- 输入框 -->
		<user-chat-bottom @submit="submit"></user-chat-bottom>
	</view>
</template>

<script>
	import userChatBottom from '../../components/user-chat/user-chat-bottom.vue';
	import time from "../../common/time.js";
	import userChatList from '../../components/user-chat-list/user-chat-list.vue';
	export default {
		components:{
			userChatBottom,
			userChatList
		},
		data() {
			return {
				scrollTop:0,
				style:{
					contentH:0,
					itemH:0
				},
				list:[]
			}
		},
		onLoad() {
			this.getdata();
			this.initdata();
		},
		methods: {
			// 获取聊天数据
			getdata(){
				// 从服务器获取到的数据
				let arr=[
					{
						isme:false,
						userpic:"../../static/demo/userpic/11.jpg",
						type:"text",
						data:"哈哈哈",
						time:"1555146412"
					},
					{
						isme:true,
						userpic:"../../static/demo/userpic/10.jpg",
						type:"img",
						data:"../../static/demo/3.jpg",
						time:"1555146414",
					},
				];
				for (let i = 0; i < arr.length; i++) {
					arr[i].gstime=time.gettime.getChatTime(arr[i].time,i>0?arr[i-1].time:0);
				}
				this.list=arr;
			},
			submit(data){
				console.log(data)
				// 构建数据
				let now=new Date().getTime();
				let obj={
					isme:true,
					userpic:"../../static/demo/userpic/10.jpg",
					type:"text",
					data:data,
					time:now,
					gstime:time.gettime.getChatTime(now,this.list[this.list.length-1].time)
				};
				this.list.push(obj);
				this.scrollToBottom()
			},
			initdata(){
				try {
					const res = uni.getSystemInfoSync();
					this.style.contentH=res.windowHeight - uni.upx2px(120);
				} catch (e) { }
			},
			scrollToBottom(){
				const query = uni.createSelectorQuery();
				query.selectAll('.user-chat-item').boundingClientRect(data => {
				  console.log("得到布局位置信息" + JSON.stringify(data));
				  console.log("节点离页面顶部的距离为" + data.top);
				}).exec();
			}
		}
	}
</script>

<style>
.user-chat-list>image{
	width: 100upx;
	height: 100upx;
	border-radius: 100%;
	flex-shrink: 0;
}
.user-chat-list-body{
	position: relative;
	background: #F4F4F4;
	padding: 25upx;
	margin-left: 20upx;
	border-radius: 20upx;
	margin-right: 100upx;
}
.user-chat-list-body:after{
	position: absolute;
	left: -30upx;
	right: 0;
	top: 30upx;
	content: '';
	width: 0;
	height: 0;
	border: 16upx solid #F4F4F4;
	border-color: transparent #F4F4F4 transparent transparent;
}
.user-chat-me{
	justify-content: flex-end;
}
.user-chat-me .user-chat-list-body{
	margin-right: 20upx;
	margin-left: 100upx;
}
.user-chat-me .user-chat-list-body:after{
	left: auto;
	right: -30upx;
	border-color: transparent transparent transparent #F4F4F4;
}
.user-chat-list-body>image{
	max-width: 150upx;
	max-height: 200upx;
}
</style>
