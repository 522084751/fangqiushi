<template>
	<view class="body">
		<!-- 导航无法去掉左边返回按钮 -->
		<!-- tab切换 -->
		<swiper-tab-head 
			:tabBars="tabBars" 
			:tabIndex="tabIndex"
			@tabtap="tabtap"
			scrollItemStyle="width:33%;"
			scrollStyle="border-bottom:0;">			
		</swiper-tab-head>
		
		<!-- 好友列表 -->
		<!-- <block v-for="(item,index) in list" :key="index">
			<user-list :item="item" :index="index"></user-list>
		</block> -->
		
		<view class="uni-tab-bar">
		<swiper class="swiper-box" 
				:style="{height:swiperheight+'px'}" 
				:current="tabIndex"
				@change="tabChange">
			<swiper-item v-for="(items,index) in newslist" :key="index">
				<scroll-view scroll-y class="list" @scrolltolower="loadmore(index)">
					<template v-if="items.list.length>0">
						<!-- 图文列表 -->
						<block v-for="(item,index1) in items.list" :key="index1">
							<user-list :item="item" :index="index1"></user-list>
						</block>
						<!-- 上拉加载 -->
						<load-more :loadtext="items.loadtext"></load-more>
					</template>
					<template v-else>
						<!-- 无内容默认 -->
						<no-thing></no-thing>
					</template>
				</scroll-view>
			</swiper-item>
		</swiper>
		</view>
	</view>
</template>

<script>
	import swiperTabHead from '../../components/index/swiper-tab-head.vue';
	import userList from '../../components/user-list/user-list.vue';
	import loadMore from "../../components/common/load-more.vue";
	import noThing from "../../components/common/no-thing.vue";
	export default {
		components:{
			swiperTabHead,
			userList,
			loadMore,
			noThing
		},
		data() {
			return {
				swiperheight: 0,
				tabIndex: 0,
				tabBars:[
					{name:"互关",id:"huguan",num:10 },
					{name:"关注",id:"guanzhu",num:20 },	
					{name:"粉丝",id:"fensi",num:30 },
				],
				newslist: [
					{
						loadtext: "上拉加载更多",
						list: [
							{
								userpic: "../../static/demo/userpic/10.jpg",
								username: "昵称11",
								age: 20,
								sex: 0,  //0nan 1nv
								isguanzhu: false
							},{
								userpic: "../../static/demo/userpic/10.jpg",
								username: "昵称12",
								age: 18,
								sex: 1,  //0nan 1nv
								isguanzhu: true
							}
						]
					},{
						loadtext: "上拉加载更多",
						list: [
							{
								userpic: "../../static/demo/userpic/10.jpg",
								username: "昵称21",
								age: 20,
								sex: 0,  //0nan 1nv
								isguanzhu: false
							},{
								userpic: "../../static/demo/userpic/10.jpg",
								username: "昵称22",
								age: 18,
								sex: 1,  //0nan 1nv
								isguanzhu: true
							},
							{
								userpic: "../../static/demo/userpic/10.jpg",
								username: "昵称23",
								age: 20,
								sex: 0,  //0nan 1nv
								isguanzhu: false
							},{
								userpic: "../../static/demo/userpic/10.jpg",
								username: "昵称24",
								age: 18,
								sex: 1,  //0nan 1nv
								isguanzhu: true
							}
						]
					},{
						loadtext: "上拉加载更多",
						list: [
							{
								userpic: "../../static/demo/userpic/10.jpg",
								username: "昵称3",
								age: 20,
								sex: 0,  //0nan 1nv
								isguanzhu: false
							}
						]
					}
				]
				
			}
		},
		onLoad() {
			uni.getSystemInfo({
				success: (res) =>{
					let height=res.windowHeight-uni.upx2px(100);
					this.swiperheight = height;
				}
			});
		},
		// 监听导航按钮事件
		onNavigationBarButtonTap(e){
			if(e.index == 0){
				uni.navigateBack({
					delta: 1
				})
			}
		},
		methods: {
			// 上拉加载
			loadmore(index){
				if(this.newslist[index].loadtext!="上拉加载更多"){
					return;
				}
				//修改状态
				this.newslist[index].loadtext="加载中...";
				// 获取数据
				setTimeout(()=>{
					//获取完成
					let obj={
						userpic: "../../static/demo/userpic/10.jpg",
						username: "昵称51",
						age: 20,
						sex: 0,  //0nan 1nv
						isguanzhu: false
					};
					this.newslist[index].list.push(obj);
					this.newslist[index].loadtext="上拉加载更多";
				}, 1000)
			},
			//tabbar点击事件
			tabtap(index){
				console.log(index);
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
.body{
	/* padding: 0 20upx; */
}

	
</style>
