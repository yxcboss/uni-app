<template>
	<view>
		<!-- tabbar切换 -->
		<swiper-tab-head 
		:tabBars="tabBars" 
		:tabIndex="tabIndex"
		@tabtap="tabtap"
		scrollItemStyle="width:33.3%;"
		scrollStyle="border-bottom:0;">
		</swiper-tab-head>
		
		<!-- 好友列表 -->
		<!-- <block v-for="(item,index) in newslist" :key="index">
			<user-list :item="item" :index="index"></user-list>
		</block> -->
		
		<view class="uni-tab-bar">
		<swiper class="swiper-box" 
		:style="{height:swiperheight+'px'}" 
		:current="tabIndex"
		@change="tabChange">
			<swiper-item v-for="(items,index) in newslist" :key="index"> 
				<scroll-view scroll-y class="list" @scrolltolower='loadmore(index)'>
					<template v-if="items.list.length>0">
						<block v-for="(item,index1) in items.list" :key="index1">
							<user-list :item="item" :index="index"></user-list>
						</block>
						<uni-load-more showImage="true" :status ='loadmorestatus'></uni-load-more>
					</template>
					<template v-else>
						<noThing></noThing>
					</template>
				</scroll-view>
			</swiper-item>
		</swiper>   
		</view>
	</view>
</template>

<script>
	import swiperTabHead from "../../components/index/swiper-tab-head.vue";
	import userList from '../../components/user-list/user-list.vue';
	import uniLoadMore from "../../components/uni-load-more/uni-load-more.vue";
	import noThing from '../../components/common/no-thing.vue'
	export default {
		components:{
			userList,
			swiperTabHead,
			uniLoadMore,
			noThing
		},
		data() {
			return {
				loadmorestatus:"more",
				swiperheight:500,
				tabIndex:0,
				tabBars:[
					{ name:"互关",id:"huguan",num:10 },
					{ name:"关注",id:"guanzhu",num:20 },
					{ name:"粉丝",id:"fensi",num:30 },
				],
				
				newslist:[
					{
						loadtext:"上拉加载更多",
						list:[
							{
								userpic:"../../static/demo/userpic/11.jpg",
								username:"昵称",
								age:20,
								sex:0,
								isguanzhu:true
							},
							{
								userpic:"../../static/demo/userpic/11.jpg",
								username:"昵称",
								age:21,
								sex:1,
								isguanzhu:false
							},
							{
								userpic:"../../static/demo/userpic/11.jpg",
								username:"昵称",
								age:20,
								sex:0,
								isguanzhu:true
							},
							{
								userpic:"../../static/demo/userpic/11.jpg",
								username:"昵称",
								age:21,
								sex:1,
								isguanzhu:false
							},
							{
								userpic:"../../static/demo/userpic/11.jpg",
								username:"昵称",
								age:20,
								sex:0,
								isguanzhu:true
							},
							{
								userpic:"../../static/demo/userpic/11.jpg",
								username:"昵称",
								age:21,
								sex:1,
								isguanzhu:false
							},
							{
								userpic:"../../static/demo/userpic/11.jpg",
								username:"昵称",
								age:20,
								sex:0,
								isguanzhu:true
							},
							{
								userpic:"../../static/demo/userpic/11.jpg",
								username:"昵称",
								age:21,
								sex:1,
								isguanzhu:false
							}
						]
					},
					{
						loadtext:"上拉加载更多",
						list:[
							{
								userpic:"../../static/demo/userpic/11.jpg",
								username:"昵称",
								age:20,
								sex:0,
								isguanzhu:true
							},
							{
								userpic:"../../static/demo/userpic/11.jpg",
								username:"昵称",
								age:21,
								sex:1,
								isguanzhu:false
							}
						]
					},
					{
						loadtext:"上拉加载更多",
						list:[
							{
								userpic:"../../static/demo/userpic/11.jpg",
								username:"昵称",
								age:20,
								sex:0,
								isguanzhu:true
							},
							{
								userpic:"../../static/demo/userpic/11.jpg",
								username:"昵称",
								age:21,
								sex:1,
								isguanzhu:false
							}
						]
					}
				]
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
		onLoad() {
			uni.getSystemInfo({
				success: (res)=> {
					let height=res.windowHeight-uni.upx2px(100)
					this.swiperheight=height;
				}
			});
		},
		methods: {
			// tabbar点击事件
			tabtap(index){
				this.tabIndex=index;
			},
			// 滑动事件
			tabChange(e){
				this.tabIndex=e.detail.current;
			},
			// 上拉加载
			loadmore(index){
				this.loadmorestatus = 'loading';
				// 获取数据
				setTimeout(()=> {
					//获取完成
					let obj={
						userpic:"../../static/demo/userpic/11.jpg",
						username:"昵称",
						age:20,
						sex:0,
						isguanzhu:true
					};
					this.newslist[index].list.push(obj);
					this.loadmorestatus = 'more'
				}, 1000);
			}
		}
	}
</script>

<style>
	
</style>
