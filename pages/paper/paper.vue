<template>
	<view class="body">
		<!-- 操作菜单 -->
		<paper-left-popup 
			:show="show"
			@hide="hidepopup"
			@addfriend="addfriend"
			@clear="clear">
		</paper-left-popup>
		<!-- 小纸条列表 -->
		<block v-for="(item,index) in list" :key="index">
			<paper-list :item="item" :index="index"></paper-list>
		</block>
	
		<!-- 上拉加载 -->
		<load-more :loadtext="loadtext"></load-more>
	</view>
</template>

<script>

	import paperList from '../../components/paper/paper-list.vue';
	import loadMore from "../../components/common/load-more.vue";
	import paperLeftPopup from '../../components/paper/paper-left-popup.vue';
	export default {
		components:{
			paperList,
			loadMore,
			paperLeftPopup
		},
		data() {
			return {
				show: false,
				loadtext: "上拉加载更多",
				list: [
					{
						userpic: "../../static/demo/userpic/2.jpg",
						username: "昵称1",
						time: "10:21",
						data: "我是信息1",
						noreadnum: 2
					},{
						userpic: "../../static/demo/userpic/1.jpg",
						username: "昵称2",
						time: "10:21",
						data: "我是信息2",
						noreadnum: 0
					},{
						userpic: "../../static/demo/userpic/3.jpg",
						username: "昵称3",
						time: "10:21",
						data: "我是信息3",
						noreadnum: 0
					},{
						userpic: "../../static/demo/userpic/4.jpg",
						username: "昵称4",
						time: "10:21",
						data: "我是信息4",
						noreadnum: 11
					},{
						userpic: "../../static/demo/userpic/5.jpg",
						username: "昵称5",
						time: "10:21",
						data: "我是信息5",
						noreadnum: 0
					},{
						userpic: "../../static/demo/userpic/6.jpg",
						username: "昵称6",
						time: "10:21",
						data: "我是信息6",
						noreadnum: 11
					},{
						userpic: "../../static/demo/userpic/7.jpg",
						username: "昵称7",
						time: "10:21",
						data: "我是信息7",
						noreadnum: 0
					},{
						userpic: "../../static/demo/userpic/8.jpg",
						username: "昵称8",
						time: "10:21",
						data: "我是信息8",
						noreadnum: 11
					}
				]
			}
		},
		//监听导航按钮点击事件
		onNavigationBarButtonTap(e) {
			console.log(JSON.stringify(e));
			switch (e.index){
				case 0:
				console.log("点击了左边按钮");
				uni.navigateTo({
					url: "../user-list/user-list",
				});
				this.hidepopup();
					break;
				case 1:
				this.showpopup();
					break;
			}
		},
		//监听下拉刷新
		onPullDownRefresh(){
			this.getdata();
		},
		//监听上拉加载
		onReachBottom(){
			this.loadmore();
		},
		methods: {
			//操作菜单
			addfriend(){
				console.log("加糗友");
				this.hidepopup();
			},
			clear(){
				console.log("清除缓存");
				this.hidepopup();
			},
			hidepopup(){
				this.show=false;
			},
			showpopup(){
				this.show=true;
			},
			// 上拉加载
			loadmore(index){
				if(this.loadtext!="上拉加载更多"){
					return;
				}
				//修改状态
				this.loadtext="加载中...";
				// 获取数据
				setTimeout(()=>{
					//获取完成
					let obj={
							userpic: "../../static/demo/userpic/2.jpg",
							username: "昵称2354",
							time: "10:21",
							data: "我是信息12354",
							noreadnum: 2
						}
					this.list.push(obj);
					this.loadtext="上拉加载更多";
				}, 1000)
			},
			//获取数据
			getdata(){
				setTimeout(()=>{				
					//模拟服务器获取数据
					let arr = [
						{
							userpic: "../../static/demo/userpic/2.jpg",
							username: "昵称1111",
							time: "10:21",
							data: "我是信息1111",
							noreadnum: 2
						},{
							userpic: "../../static/demo/userpic/1.jpg",
							username: "昵称2222",
							time: "10:21",
							data: "我是信息2222",
							noreadnum: 0
						},{
							userpic: "../../static/demo/userpic/3.jpg",
							username: "昵称3333",
							time: "10:21",
							data: "我是信息3333",
							noreadnum: 0
						},{
							userpic: "../../static/demo/userpic/4.jpg",
							username: "昵称4444",
							time: "10:21",
							data: "我是信息44444",
							noreadnum: 11
						}
					]
					//赋值
					this.list = arr;
					//关闭下拉刷新
					uni.stopPullDownRefresh();
				},2000)
			}
		}
	}
</script>

<style>
.body{
	padding: 0 20upx;
}

</style>
