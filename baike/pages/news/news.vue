<template>
	<view>
		<!-- 自定义导航栏 -->
		<new-nav-bar :tabBars="tabBars" :tabIndex="tabIndex" @change-tab="changeTab" />

		<view class="uni-tab-bar">
			<swiper class="swiper-box" :style="{height:swiperheight+'px'}" :current="tabIndex" @change="tabChange">
				<swiper-item>
					<scroll-view scroll-y class="list" @scrolltolower='loadmore()'>
						<!-- 列表 -->
						<block v-for="(item,index) in guanzhu.list" :key="index">
							<common-list :item="item" :index="index"></common-list>
						</block>
						<uni-load-more showImage="true" :status='loadmorestatus'></uni-load-more>
					</scroll-view>
				</swiper-item>
				<swiper-item>
					<scroll-view scroll-y class="list">
						<!-- 搜索框 -->
						<view class="search-input">
							<input type="text" placeholder-class="icon iconfont icon-sousuo topic-search" placeholder="搜索内容" />
						</view>
						<!-- 轮播图 -->
						<swiper class="topic-swiper" :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
							<block v-for="(item,index) in topic.swiper" :key="index">
								<swiper-item>
									<image :src="item.src" mode="widthFix" lazy-load></image>
								</swiper-item>
							</block>
						</swiper>
						<!-- 热门分类 -->
						<topic-nav :nav="topic.nav"></topic-nav>
						<!-- 最近更新 -->
						<view class="topic-new">
							<view>最近更新</view>
							<block v-for="item in topic.list">
								<topic-list :item="item"></topic-list>
							</block>
						</view>
					</scroll-view>
				</swiper-item>
			</swiper>
		</view>

	</view>
</template>

<script>
	import newNavBar from '../../components/news/new-nav-bar.vue'
	import commonList from '../../components/common/common-list.vue'
	import uniLoadMore from "../../components/uni-load-more/uni-load-more.vue";
	import topicNav from '../../components/news/topic-nav.vue'
	import topicList from '../../components/news/topic-list.vue'
	export default {
		components: {
			commonList,
			newNavBar,
			uniLoadMore,
			topicNav,
			topicList
		},
		data() {
			return {
				loadmorestatus: "more",
				swiperheight: 500,
				tabIndex: 0,
				tabBars: [{
						name: "关注",
						id: "guanzhu"
					},
					{
						name: "话题",
						id: "topic"
					}
				],
				guanzhu: {
					list: [
						// 文字
						{
							userpic: "../../static/demo/userpic/12.jpg",
							username: "哈哈",
							sex: 0, //0 男 1 女
							age: 25,
							isguanzhu: false,
							title: "我是标题",
							titlepic: "",
							video: false,
							share: false,
							path: "深圳 龙岗",
							sharenum: 20,
							commentnum: 30,
							goodnum: 20
						},
						// 图文
						{
							userpic: "../../static/demo/userpic/12.jpg",
							username: "哈哈",
							sex: 0, //0 男 1 女
							age: 25,
							isguanzhu: false,
							title: "我是标题",
							titlepic: "../../static/demo/datapic/13.jpg",
							video: false,
							share: false,
							path: "深圳 龙岗",
							sharenum: 20,
							commentnum: 30,
							goodnum: 20
						},
						// 视频
						{
							userpic: "../../static/demo/userpic/12.jpg",
							username: "哈哈",
							sex: 0, //0 男 1 女
							age: 25,
							isguanzhu: false,
							title: "我是标题",
							titlepic: "../../static/demo/datapic/13.jpg",
							video: {
								looknum: "20w",
								long: "2:47"
							},
							share: false,
							path: "深圳 龙岗",
							sharenum: 20,
							commentnum: 30,
							goodnum: 20
						},
						// 分享
						{
							userpic: "../../static/demo/userpic/12.jpg",
							username: "哈哈",
							sex: 0, //0 男 1 女
							age: 25,
							isguanzhu: false,
							title: "我是标题",
							titlepic: "",
							video: false,
							share: {
								title: "我是分享的标题",
								titlepic: "../../static/demo/datapic/14.jpg"
							},
							path: "深圳 龙岗",
							sharenum: 20,
							commentnum: 30,
							goodnum: 20
						},
					]
				},
				topic: {
					swiper: [{
							src: "../../static/demo/banner2.jpg"
						},
						{
							src: "../../static/demo/banner2.jpg"
						},
						{
							src: "../../static/demo/banner2.jpg"
						},
					],
					nav: [{
							name: "最新"
						},
						{
							name: "游戏"
						},
						{
							name: "打卡"
						},
						{
							name: "情感"
						},
						{
							name: "故事"
						},
						{
							name: "喜爱"
						},
					],
					list: [{
							titlepic: "../../static/demo/topicpic/13.jpeg",
							title: "话题名称",
							desc: "我是话题描述",
							totalnum: 50,
							todaynum: 10
						},
						{
							titlepic: "../../static/demo/topicpic/13.jpeg",
							title: "话题名称",
							desc: "我是话题描述",
							totalnum: 50,
							todaynum: 10
						},
						{
							titlepic: "../../static/demo/topicpic/13.jpeg",
							title: "话题名称",
							desc: "我是话题描述",
							totalnum: 50,
							todaynum: 10
						},
						{
							titlepic: "../../static/demo/topicpic/13.jpeg",
							title: "话题名称",
							desc: "我是话题描述",
							totalnum: 50,
							todaynum: 10
						},
						{
							titlepic: "../../static/demo/topicpic/13.jpeg",
							title: "话题名称",
							desc: "我是话题描述",
							totalnum: 50,
							todaynum: 10
						},
						{
							titlepic: "../../static/demo/topicpic/13.jpeg",
							title: "话题名称",
							desc: "我是话题描述",
							totalnum: 50,
							todaynum: 10
						}
					]
				}
			}
		},
		onLoad() {
			uni.getSystemInfo({
				success: (res) => {
					let height = res.windowHeight - uni.upx2px(100)
					this.swiperheight = height;
				}
			});
		},
		methods: {
			changeTab(index) {
				console.log(index);
				this.tabIndex = index;
			},
			// 滑动事件
			tabChange(e) {
				this.tabIndex = e.detail.current;
			},
			// 上拉加载
			loadmore(index) {
				this.loadmorestatus = 'loading'
				setTimeout(() => {
					//获取完成
					let obj = {
						userpic: "../../static/demo/userpic/12.jpg",
						username: "哈哈",
						sex: 0, //0 男 1 女
						age: 25,
						isguanzhu: false,
						title: "我是标题",
						titlepic: "../../static/demo/datapic/13.jpg",
						video: false,
						share: false,
						path: "深圳 龙岗",
						sharenum: 20,
						commentnum: 30,
						goodnum: 20
					};
					this.guanzhu.list.push(obj);
					this.loadmorestatus = 'more'
				}, 1000);
				console.log(index)
			}
		}
	}
</script>

<style>
	.search-input {
		padding: 20upx;
	}

	.search-input>input {
		background: #F4F4F4;
		border-radius: 10upx;
	}

	.topic-search {
		display: flex;
		justify-content: center;
		font-size: 27upx;
	}

	.topic-swiper {
		padding: 0 20upx 20upx 20upx;
	}

	.topic-swiper image {
		width: 100%;
		border-radius: 10upx;
	}

	.topic-new {
		padding: 20upx;
	}

	.topic-new>view:first-child {
		padding-bottom: 10upx;
		font-size: 32upx;
	}

	.topic-list {
		padding: 10upx 0;
		border-bottom: 1upx solid #EEEEEE;
	}

	.topic-list image {
		width: 150upx;
		height: 150upx;
		border-radius: 10upx;
		margin-right: 20upx;
	}

	.topic-list>view>view {
		color: #A4A4A4;
	}

	.topic-list>view>view:first-child {
		color: #333333;
		font-size: 32upx;
	}
</style>
