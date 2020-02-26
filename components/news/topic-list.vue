
<template>
	<view class="topic-list u-f animated fadeIn-left fast" @tap="opendetail">
		<image :src="item.titlepic" mode="widthFix" lazy-load=""></image>
		<view class="">
			<view>{{item.title}}</view>
			<view>{{item.desc}}</view>
			<view>动态 {{item.totalnum}}  今日 {{item.todaynum}}</view>
		</view>
	</view>
</template>

<script>
	export default {
		props:{
			item: Object,
			index: Number
		},
		methods:{
			opendetail(){
				uni.navigateTo({
					url: '../../pages/topic-detail/topic-detail',
				});
			}
		}
	}
</script>

<style scoped>
	/* 话题列表 */
	.topic-new{
		padding: 20upx;
	}
	.topic-new>view:first-child{
		padding-bottom: 5upx;
		font-size: 32upx;
		color: #333;
	}
	.topic-list{
		padding: 20upx 0;
		border-bottom: 1upx solid #EEEEEE;
	}
	.topic-list image{
		width: 150upx!important;
		height: 150upx!important;
		border-radius: 10upx;
		margin-right: 20upx;
	}
	.topic-list>view>view{
		color: #A4A4A4;
	}
	.topic-list>view>view:first-child{
		font-size: 32upx;
		color: #333;
	}
</style>
