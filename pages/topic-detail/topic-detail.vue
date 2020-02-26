<template>
	<view>
		<!-- 话题介绍 -->
		<topic-info :item="topicInfo"></topic-info>
		<!-- tabbar切换 -->
		<swiper-tab-head 
			:tabBars="tabBars" 
			:tabIndex="tabIndex"
			@tabtap="tabtap"
			scrollItemStyle="width:50%;"
			scrollStyle="border-bottom:0">			
		</swiper-tab-head>
		<!-- 列表 -->
		<view class="topic-detail-list">
			<block v-for="(item, index) in tablist" :key="index">
				<template v-if="tabIndex==index">
					<!-- 列表 -->
					<block v-for="(list,listindex) in item.list" :key="listindex">
						<common-list :item="list" :index="listindex"></common-list>
					</block>
					<!-- 上拉加载 -->
					<load-more :loadtext="item.loadtext"></load-more>
				</template>
			</block>
		</view>
		<view>
			
		</view>
	</view>
</template>

<script>
	import topicInfo from "../../components/topic/topic-info.vue";
	import swiperTabHead from '../../components/index/swiper-tab-head.vue';
	import commonList from '../../components/common/common-list.vue';
	import loadMore from "../../components/common/load-more.vue";
	export default {
		components:{
			topicInfo,
			swiperTabHead,
			commonList,
			loadMore
		},
		data() {
			return {
				topicInfo: {
					titlepic: "../../static/demo/topicpic/13.jpeg",
					title: "忆往事，敬余生",
					desc: "我是描述",
					totalnum: 1000,
					todaynum: 1000,
				},
				tabIndex: 0,
				tabBars:[
					{name:"默认",id:"moren" },
					{name:"最新",id:"zuixin" }					
				],
				tablist: [
					{
						loadtext:"上拉加载更多",
						list: [
							//文字
							{
								userpic: "../../static/demo/userpic/12.jpg",
								username: "哈哈哈",
								sex: 0, //0男 1女
								age: 25,
								isguanzhu: false,
								title: "我是标题",
								titlepic: "", //图片
								video: false, //视频
								share: false, //分享
								path: "深圳 龙岗",
								sharenum: 20,
								commentnum: 30,
								goodnum: 20, //点赞数
							},
							//图文
							{
								userpic: "../../static/demo/userpic/12.jpg",
								username: "哈哈哈",
								sex: 1, //0男 1女
								age: 25,
								isguanzhu: false,
								title: "我是标题",
								titlepic: "../../static/demo/datapic/14.jpg", //图片
								video: false, //视频
								share: false, //分享
								path: "深圳 龙岗",
								sharenum: 20,
								commentnum: 30,
								goodnum: 20, //点赞数
							},
							//视频
							{
								userpic: "../../static/demo/userpic/12.jpg",
								username: "哈哈哈",
								sex: 1, //0男 1女
								age: 25,
								isguanzhu: false,
								title: "我是标题",
								titlepic: "../../static/demo/datapic/13.jpg", //图片
								video: {
									looknum: "20w",
									long: "2:47"
								}, //视频
								share: false, //分享
								path: "深圳 龙岗",
								sharenum: 20,
								commentnum: 30,
								goodnum: 20, //点赞数
							},
							//分享
							{
								userpic: "../../static/demo/userpic/12.jpg",
								username: "哈哈哈",
								sex: 0, //0男 1女
								age: 25,
								isguanzhu: false,
								title: "我是标题",
								titlepic: "", //图片
								video: false, //视频
								share: {
									title: "我是标题",
									titlepic: "../../static/demo/datapic/14.jpg"
								}, //分享
								path: "深圳 龙岗",
								sharenum: 20,
								commentnum: 30,
								goodnum: 20, //点赞数
							}
						]
					},{
						loadtext:"上拉加载更多",
						list: [
							//文字
							{
								userpic: "../../static/demo/userpic/12.jpg",
								username: "哈哈哈",
								sex: 0, //0男 1女
								age: 25,
								isguanzhu: false,
								title: "我是标题",
								titlepic: "", //图片
								video: false, //视频
								share: false, //分享
								path: "深圳 龙岗",
								sharenum: 20,
								commentnum: 30,
								goodnum: 20, //点赞数
							},
							//图文
							{
								userpic: "../../static/demo/userpic/12.jpg",
								username: "哈哈哈",
								sex: 1, //0男 1女
								age: 25,
								isguanzhu: false,
								title: "我是标题",
								titlepic: "../../static/demo/datapic/14.jpg", //图片
								video: false, //视频
								share: false, //分享
								path: "深圳 龙岗",
								sharenum: 20,
								commentnum: 30,
								goodnum: 20, //点赞数
							},
							//视频
							{
								userpic: "../../static/demo/userpic/12.jpg",
								username: "哈哈哈",
								sex: 1, //0男 1女
								age: 25,
								isguanzhu: false,
								title: "我是标题",
								titlepic: "../../static/demo/datapic/13.jpg", //图片
								video: {
									looknum: "20w",
									long: "2:47"
								}, //视频
								share: false, //分享
								path: "深圳 龙岗",
								sharenum: 20,
								commentnum: 30,
								goodnum: 20, //点赞数
							},
							//分享
							{
								userpic: "../../static/demo/userpic/12.jpg",
								username: "哈哈哈",
								sex: 0, //0男 1女
								age: 25,
								isguanzhu: false,
								title: "我是标题",
								titlepic: "", //图片
								video: false, //视频
								share: {
									title: "我是标题",
									titlepic: "../../static/demo/datapic/14.jpg"
								}, //分享
								path: "深圳 龙岗",
								sharenum: 20,
								commentnum: 30,
								goodnum: 20, //点赞数
							}
						]
					}
				]
			}
		},
		//上拉触底事件
		onReachBottom() {
			console.log("1111111111");
			//上拉加载
			this.loadmore();
		},
		//监听下拉刷新
		onPullDownRefresh() {
			
			this.getdata();
		},
		methods: {
			//下拉刷新
			getdata(){
				setTimeout(()=>{
					//获取数据
					let arr=[
						//文字
							{
								userpic: "../../static/demo/userpic/12.jpg",
								username: "哈哈哈111",
								sex: 0, //0男 1女
								age: 25,
								isguanzhu: false,
								title: "我是标题1111",
								titlepic: "", //图片
								video: false, //视频
								share: false, //分享
								path: "深圳 龙岗",
								sharenum: 20,
								commentnum: 30,
								goodnum: 20, //点赞数
							},
							//图文
							{
								userpic: "../../static/demo/userpic/12.jpg",
								username: "哈哈哈222",
								sex: 1, //0男 1女
								age: 25,
								isguanzhu: false,
								title: "我是标题222",
								titlepic: "../../static/demo/datapic/14.jpg", //图片
								video: false, //视频
								share: false, //分享
								path: "深圳 龙岗",
								sharenum: 20,
								commentnum: 30,
								goodnum: 20, //点赞数
							},
							//视频
							{
								userpic: "../../static/demo/userpic/10.jpg",
								username: "哈哈哈333",
								sex: 1, //0男 1女
								age: 25,
								isguanzhu: false,
								title: "我是标题3333",
								titlepic: "../../static/demo/datapic/13.jpg", //图片
								video: {
									looknum: "20w",
									long: "2:47"
								}, //视频
								share: false, //分享
								path: "深圳 龙岗",
								sharenum: 20,
								commentnum: 30,
								goodnum: 20, //点赞数
							},
							//分享
							{
								userpic: "../../static/demo/userpic/12.jpg",
								username: "哈哈哈",
								sex: 0, //0男 1女
								age: 25,
								isguanzhu: false,
								title: "我是标题",
								titlepic: "", //图片
								video: false, //视频
								share: {
									title: "我是标题",
									titlepic: "../../static/demo/datapic/14.jpg"
								}, //分享
								path: "深圳 龙岗",
								sharenum: 20,
								commentnum: 30,
								goodnum: 20, //点赞数
							}
						
					];
					
				
					//赋值
					this.tablist[this.tabIndex].list = arr;
					//关闭下拉刷新
					
						uni.stopPullDownRefresh();//2秒停止刷新转圈圈
					},2000)
			
			},
			//上拉加载
			loadmore(index){
				if(this.tablist[this.tabIndex].loadtext!="上拉加载更多"){
					return;
				}
				//修改状态
				this.tablist[this.tabIndex].loadtext="加载中...";
				// 获取数据
				setTimeout(()=>{
					//获取完成
					let obj={
						userpic:"../../static/demo/userpic/5.jpg",
						username:"昵称",
						isguanzhu:true,
						title:"我是标题",
						type:"video", //img是图文类型，video是视频类型
						playnum:"20w",
						long:"2:47",
						titlepic:"../../static/demo/datapic/8.jpg",
						goodnum: 50, //点赞数
						commentnum:30,
						sharenum:40
					};
					this.tablist[this.tabIndex].list.push(obj);
					this.tablist[this.tabIndex].loadtext="上拉加载更多";
				}, 1000)
			},
			
			//tabbar点击事件
			tabtap(index){
				this.tabIndex=index;
			},
			//滑动事件
			tabChange(e){
				this.tabIndex = e.detail.current;
			}
		}
	}
</script>

<style>

</style>
