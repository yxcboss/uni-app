<template>
	<view class="content" style="overflow: hidden;">
      
	<swiper-tab-head 
	:tabBars="tabBars" 
	:tabIndex="tabIndex"
	@tabtap="tabtap">
	</swiper-tab-head>
	
	<view class="uni-tab-bar">
	<swiper class="swiper-box" 
	:style="{height:swiperheight+'px'}" 
	:current="tabIndex"
	@change="tabChange">
		<swiper-item v-for="(items,index) in newslist" :key="index"> 
			<scroll-view scroll-y class="list" @scrolltolower='loadmore(index)'>
				<template v-if="items.list.length>0">
					<block v-for="(item,index1) in items.list" :key="index1">
						<index-list :item="item" :index="index1"></index-list>
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
	import indexList from "../../components/index/index-list.vue";
	import swiperTabHead from "../../components/index/swiper-tab-head.vue";
	import uniLoadMore from "../../components/uni-load-more/uni-load-more.vue";
	import noThing from '../../components/common/no-thing.vue'
	export default {
		components:{
			indexList,
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
					{ name:"关注",id:"guanzhu" },
					{ name:"推荐",id:"tuijian" },
					{ name:"体育",id:"tiyu" 	  },
					{ name:"热点",id:"redian"  },
					{ name:"财经",id:"caijing" },
					{ name:"娱乐",id:"yule"    },
				],	
				newslist:[
					{
						list:[
							{
								userpic:"../../static/demo/userpic/12.jpg",
								username:"昵称",
								isguanzhu:false,
								title:"我是标题",
								type:"img", // img:图文,video:视频
								titlepic:"../../static/demo/datapic/11.jpg",
								infonum:{
									index:0,//0:没有操作，1:顶,2:踩；
									dingnum:11,
									cainum:11,
								},
								commentnum:10,
								sharenum:10,
							},
							{
								userpic:"../../static/demo/userpic/12.jpg",
								username:"昵称",
								isguanzhu:true,
								title:"我是标题",
								type:"video", // img:图文,video:视频
								titlepic:"../../static/demo/datapic/11.jpg",
								playnum:"20w",
								long:"2:47",
								infonum:{
									index:1,//0:没有操作，1:顶,2:踩；
									dingnum:11,
									cainum:11,
								},
								commentnum:10,
								sharenum:10,
							}
						]
					},
					{
						list:[
							{
								userpic:"../../static/demo/userpic/12.jpg",
								username:"昵称",
								isguanzhu:false,
								title:"我是标题",
								type:"img", // img:图文,video:视频
								titlepic:"../../static/demo/datapic/11.jpg",
								infonum:{
									index:0,//0:没有操作，1:顶,2:踩；
									dingnum:11,
									cainum:11,
								},
								commentnum:10,
								sharenum:10,
							},
							{
								userpic:"../../static/demo/userpic/12.jpg",
								username:"昵称",
								isguanzhu:true,
								title:"我是标题",
								type:"video", // img:图文,video:视频
								titlepic:"../../static/demo/datapic/11.jpg",
								playnum:"20w",
								long:"2:47",
								infonum:{
									index:1,//0:没有操作，1:顶,2:踩；
									dingnum:11,
									cainum:11,
								},
								commentnum:10,
								sharenum:10,
							},
							{
								userpic:"../../static/demo/userpic/12.jpg",
								username:"昵称",
								isguanzhu:false,
								title:"我是标题",
								type:"img", // img:图文,video:视频
								titlepic:"../../static/demo/datapic/11.jpg",
								infonum:{
									index:0,//0:没有操作，1:顶,2:踩；
									dingnum:11,
									cainum:11,
								},
								commentnum:10,
								sharenum:10,
							},
							{
								userpic:"../../static/demo/userpic/12.jpg",
								username:"昵称",
								isguanzhu:true,
								title:"我是标题",
								type:"video", // img:图文,video:视频
								titlepic:"../../static/demo/datapic/11.jpg",
								playnum:"20w",
								long:"2:47",
								infonum:{
									index:1,//0:没有操作，1:顶,2:踩；
									dingnum:11,
									cainum:11,
								},
								commentnum:10,
								sharenum:10,
							}
						]
					},
					{
						list:[
							{
								userpic:"../../static/demo/userpic/12.jpg",
								username:"昵称",
								isguanzhu:false,
								title:"我是标题",
								type:"img", // img:图文,video:视频
								titlepic:"../../static/demo/datapic/11.jpg",
								infonum:{
									index:0,//0:没有操作，1:顶,2:踩；
									dingnum:11,
									cainum:11,
								},
								commentnum:10,
								sharenum:10,
							},
							{
								userpic:"../../static/demo/userpic/12.jpg",
								username:"昵称",
								isguanzhu:true,
								title:"我是标题",
								type:"video", // img:图文,video:视频
								titlepic:"../../static/demo/datapic/11.jpg",
								playnum:"20w",
								long:"2:47",
								infonum:{
									index:1,//0:没有操作，1:顶,2:踩；
									dingnum:11,
									cainum:11,
								},
								commentnum:10,
								sharenum:10,
							},
							{
								userpic:"../../static/demo/userpic/12.jpg",
								username:"昵称",
								isguanzhu:false,
								title:"我是标题",
								type:"img", // img:图文,video:视频
								titlepic:"../../static/demo/datapic/11.jpg",
								infonum:{
									index:0,//0:没有操作，1:顶,2:踩；
									dingnum:11,
									cainum:11,
								},
								commentnum:10,
								sharenum:10,
							},
							{
								userpic:"../../static/demo/userpic/12.jpg",
								username:"昵称",
								isguanzhu:true,
								title:"我是标题",
								type:"video", // img:图文,video:视频
								titlepic:"../../static/demo/datapic/11.jpg",
								playnum:"20w",
								long:"2:47",
								infonum:{
									index:1,//0:没有操作，1:顶,2:踩；
									dingnum:11,
									cainum:11,
								},
								commentnum:10,
								sharenum:10,
							}
						]
					},
					{
						list:[]
					},
					{
						list:[]
					},
					{
						list:[]
					}
				],
				
				
			}
		},
		onLoad() {
			uni.getSystemInfo({
				success: (res)=> {
					let height=res.windowHeight-uni.upx2px(100)
					this.swiperheight=height;
				}
			});
		},
		//进入搜索页
		onNavigationBarSearchInputClicked(){
			console.log('进入搜索页')
			uni.navigateTo({
				url: '../search/search',
			});
		},
		//监听原生标题栏点击事件
		onNavigationBarButtonTap(e){
			if(e.index){
				uni.navigateTo({
					url: '../add-input/add-input',
				});
			}else{
				
			}
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
				this.loadmorestatus = 'loading'
				setTimeout(()=> {
					//获取完成
					let obj={
						userpic:"../../static/demo/userpic/12.jpg",
						username:"昵称",
						isguanzhu:false,
						title:"我是标题",
						type:"img", // img:图文,video:视频
						titlepic:"../../static/demo/datapic/11.jpg",
						infonum:{
							index:0,//0:没有操作，1:顶,2:踩；
							dingnum:11,
							cainum:11,
						},
						commentnum:10,
						sharenum:10,
					};
					this.newslist[index].list.push(obj);
					this.loadmorestatus = 'more'
					}, 1000);
				console.log(index)
			}
		},
	}
</script>

<style>
</style>
