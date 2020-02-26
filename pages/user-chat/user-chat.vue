<template>
	<view>
		<scroll-view id="scrollview" scroll-y="true" :scroll-top="scrollTop" 
					 :scroll-with-animation="true"
					 :style="{height:style.contentH + 'px'}">
			<!-- 聊天列表 -->
			<block v-for="(item,index) in list" :key="index">
				<user-chat-list :item="item" :index="index"></user-chat-list>
			</block>
		</scroll-view>
		
		
		<!-- 输入框 -->
		<user-chat-bottom @submit="submit"></user-chat-bottom>
	</view>
</template>

<script>
	import userChatBottom from '../../components/user-chat/user-chat-bottom.vue';
	import time from '../../common/time.js';
	import userChatList from '../../components/user-chat/user-chat-list.vue';
	export default {
		components:{
			userChatBottom,
			userChatList
		},
		data() {
			return {
				scrollTop: 0,
				style:{
					contentH: 0,
					itemH: 0
				},
				list:[
					{
						isme: false,
						userpic: "../../static/demo/userpic/11.jpg",
						type: "text",
						data: "你好！",
						time: "1554970014" //在线转换的时间戳
					},{
						isme: true,
						userpic: "../../static/demo/userpic/13.jpg",
						type: "img",
						data: "../../static/demo/3.jpg",
						time: "1554970014" //在线转换的时间戳
					}
					
				]
				
			}
		},
		onLoad(){
			this.getdata();
			this.initdata();
		},
		onReady() {
			this.pageToBottom();
		},
		methods: {
			//初始化参数
			initdata(){
				//接口中的系统信息
				try {
				    const res = uni.getSystemInfoSync();
					this.style.contentH = res.screenHeight - uni.upx2px(120) - uni.upx2px(88);
					console.log(this.style.contentH,'99999999999999');
					console.log(res.screenHeight,'7777777777')
				} catch (e) {
				    // error
				}
			},
			pageToBottom(){
				let q=uni.createSelectorQuery();
				q.select('#scrollview').boundingClientRect();
				q.selectAll('.user-chat-item').boundingClientRect();
				q.exec((res)=>{
					console.log(JSON.stringify(res[1]));
					res[1].forEach((ret)=>{
						console.log(ret, "*********************");
						this.style.itemH += ret.height;
					});
					if(this.style.itemH > this.style.contentH){
						this.scrollTop=this.style.itemH;
					};
				})
			},
			//获取聊天数据
			getdata(){
				//从服务器获取到的数据
				let arr=[
					{
						isme: false,
						userpic: "../../static/demo/userpic/11.jpg",
						type: "text",
						data: "你好！",
						time: "1554970014", //在线转换的时间戳
						gstime: "12:00"
					},{
						isme: true,
						userpic: "../../static/demo/userpic/13.jpg",
						type: "img",
						data: "../../static/demo/3.jpg",
						time: "1554970014", //在线转换的时间戳
						gstime: "12:00"
					}
				];
				for (let i = 0; i < arr.length; i++) {
					// arr[i].gstime=time.gettime.gettime(arr[i].time);
					arr[i].gstime=time.gettime.getChatTime(arr[i].time,i>0?arr[i-1].time:0);
				}
				this.list=arr;
			},
				
			submit(data){
				// 发送逻辑
				// console.log("当前输入的是"+data);
				//构建数据
				let now=new Date().getTime();
				let obj={
					isme: true,
					userpic: "../../static/demo/userpic/11.jpg",
					type: "text",
					data: data,
					time: now, //在线转换的时间戳
					gstime: time.gettime.getChatTime(now,this.list[this.list.length-1].time)
				};
				this.list.push(obj);
				this.pageToBottom();
				console.log(this.style.contentH,'99999999999999');
			}
		}
	}
</script>

<style>

</style>
