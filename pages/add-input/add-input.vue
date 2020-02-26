<template>
	<view>
		<!-- 自定义导航栏 -->
		<uni-nav-bar :statusBar="true" left-icon="back" right-text="发布" left-text="返回"  @click-left="back" @click-right="submit">
			<view class="u-f-ajc" style="line-height: 44px;" @tap="changelook">
				{{yinsi}}
				<view class="icon iconfont icon-xialazhankai"></view>
			</view>
		</uni-nav-bar>
		<!-- 多行输入框 -->
		<view class="uni-textarea">
			<textarea value="" placeholder="说一句话吧" v-model="text"/>
		</view>
		<!-- 上传多图 -->
		<uploud-images @tap="uploud"></uploud-images>
		<!-- 弹出公告 -->
		<uni-popup :show="showpopup" position="middle" mode="fixed" msg="" @hidePopup="hidePopup" >
			<view class="gonggao">
				<view class="u-f-ajc">
					<image src="../../static/common/addinput.png" mode=""></image>
				</view>
				<view>1、涉及黄色，政治，广告及骚扰信息</view>
				<view>2、涉及人身攻击</view>
				<view>3、留联系方式，透漏他人隐私</view>
				<view>一经核实将被封禁，情节严重者永久封禁</view>
				<button type="default" @tap="hidePopup" >朕知道了</button>
				
			</view>
			<!-- <view class="uni-center center-box">
				<image class="image" src="/static/uni.png" />
			</view> -->
		</uni-popup>
	</view>
</template>

<script>	
	let changelook =  ['所有人可见', '仅自己可见'];
	import uniNavBar from "../../components/uni-nav-bar/uni-nav-bar.vue";
	import uploudImages from '../../components/common/uploud-images.vue';
	import uniPopup from '../../components/uni-popup/uni-popup.vue';
	export default {
		components: {
			uniNavBar,
			uploudImages,
			uniPopup
		},
		data() {
			return {
				isget: false,
				showpopup: true,
				yinsi: "所有人可见",
				text: "",
				imglist: []
			};
		},
		// 监听页面返回事件
		onBackPress(){
			//如果有值
			if(!this.text && this.imglist.length < 1){
				return;
			}
			if(!this.isget){
				this.baocun();
				return true;
			}
					
		},
		
		methods: {
			//保存为草稿
			baocun(){
				uni.showModal({
					content: '是否要保存为草稿？',
					cancelText: '不保存',
					confirmText: '保存',
					success: res => {
						if(res.confirm){
							console.log("保存");
						}else{
							console.log("不保存");
						}
						this.isget = true;
						uni.navigateBack({
							delta:1
						});
					},
					
				});
			},
			// 返回事件
			back(){
				uni.navigateBack({
					delta: 1
				})
			},
			//发布 
			submit(){
				console.log("发布")
			},
			// 隐私
			changelook(){
				uni.showActionSheet({
					itemList: changelook,
					success: (res) => {
						this.yinsi = changelook[res.tapIndex]
						// console.log('选中了第' + (res.tapIndex + 1) + '个按钮');
					}
				
				});
			},
			uploud(arr){
				this.imglist=arr;
				console.log(this.imglist);
			},
			hidePopup(){
				this.showpopup = false;
			}
		}
	}
</script>

<style>
.uni-textarea{
	border: 1upx solid #eee;	
}
.gonggao{
	width: 500upx;
}
.gonggao image{
	width: 75%;
	height: 130px;
	margin-bottom: 20upx;
}
.gonggao button{
	background: #ffe934;
	color: 171606;
	margin-top: 20upx;
}
</style>
