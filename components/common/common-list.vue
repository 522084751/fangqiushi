<template>
	<view class="common-list u-f animated fadeInLeft fast">
		<view class="common-list-l">
			<image :src="item.userpic" mode="widthFix" lazy-load=""></image>
		</view>
		<view class="common-list-r">
			<view class="u-f-ac u-f-jsb">
				<view class="u-f-ac">
					{{item.username}} 
					<tag-sex-age :sex="item.sex" :age="item.age"></tag-sex-age>
					<!-- <view class="tag-sex icon iconfont"
						  :class="[item.sex == 0 ? 'icon-nan' : 'icon-nv']">
						{{item.age}}
					</view> -->
				</view>
				<view v-show="!isguanzhu" class="icon iconfont icon-zengjia" @tap="guanzhu">关注</view>
			</view>
			<view>{{item.title}}</view>
			<view class="u-f-ajc">
				<!-- 图片 -->
				<image v-if="item.titlepic" :src="item.titlepic" 
					   mode="widthFix" 
					   lazy-load=""></image>
				<!-- 视频 -->
				<template v-if="item.video">
					<view class="common-list-play icon iconfont icon-bofang"></view>
					<view class="common-list-playinfo">
						{{item.video.looknum}} 次播放 {{item.video.long}}
					</view>
				</template>
				
				<!-- 分享样式 -->
				<view class="common-list-share u-f-ac" v-if="item.share">
					<image :src="item.share.titlepic" 
						   mode="widthFix" lazy-load=""></image>
					<view>{{item.share.title}}</view>
				</view>
			</view>
			<view class="u-f-ac u-f-jsb">
				<view>{{item.path}}</view>
				<view class="u-f-ac">
					<view class="icon iconfont icon-zhuanfa">
						{{item.sharenum}}
					</view>
					<view class="icon iconfont icon-pinglun1">
						{{item.commentnum}}
					</view>
					<view class="icon iconfont icon-dianzan1">
						{{item.goodnum}}
					</view>
				</view>
			</view>			
		</view>
	</view>
</template>

<script>
	import tagSexAge from './tag-sex-age.vue';
	export default {
		components:{
			tagSexAge
		},
		props:{
			item: Object,
			index: Number
		},
		data() {
			return {
				isguanzhu: this.item.isguanzhu
			}
		},
		methods:{
			guanzhu(){
				this.isguanzhu = true;
				uni.showToast({
					title: '关注成功',
				});
			}
		}
	}
</script>

<style scoped>
	.common-list{
		padding: 20upx;
	}
	.common-list-l{
		/* 右边内容过多时防止左边被压缩 */
		flex-shrink: 0;
	}
	.common-list-l image{
		width: 90upx!important;
		height: 90upx!important;
		border-radius: 100%;
	}
	.common-list-r{
		flex: 1;
		margin-left: 15upx;
		border-bottom: 1upx solid #eee;
		padding-bottom: 10upx;
	}
	.common-list-r>view:nth-child(3) image{
		width: 100%;
		border-radius: 10upx;
	}
	.common-list-r>view:nth-child(1)>view:first-child{
		color: #999;
		font-size: 32upx;
	}
	.common-list-r>view:nth-child(1)>view:last-child{
		background: #eee;
		padding: 0 10upx;
		font-size: 26upx;
	}

	.common-list-r>view:nth-child(2){
		font-size: 32upx;
		padding: 12upx 0;
	}
	.common-list-r>view:nth-child(3){
		position: relative;
		margin-bottom: 10upx;
	}
	.common-list-play,.common-list-playinfo{
		position: absolute;
		color: #fff;
	}
	.common-list-play{
		font-size: 130upx;
	}
	.common-list-playinfo{
		right: 10upx;
		bottom: 10upx;
		background: rgba(51,51,51, 0.73);
		border-radius: 20upx;
		padding: 0 20upx;
		font-size: 26upx;
	}
	.common-list-r>view:nth-child(4)>view{
		color: #bbb;
		
	}
	.common-list-r>view:nth-child(4)>view:nth-child(2)>view{
		margin-left: 10upx;
		padding-left: 5upx;
		font-size: 28upx;
	}
	
	.common-list-share{
		background: #eee;
		width: 100%;
		padding: 10upx;
		border-radius: 10upx;
	}
	.common-list-share>image{
		width: 200upx!important;
		height: 150upx!important;
		margin-right: 10upx;
		
	}	
</style>
