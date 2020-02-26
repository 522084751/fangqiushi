<template>
	<view class="tag-sex icon iconfont"
		  :class="[sex == 0 ? 'icon-nan' : 'icon-nv']">
		{{age}}
	</view>
</template>

<script>
	export default {
		props:{
			sex:Number,
			age:Number
		}
	}
</script>

<style scoped>
.tag-sex{
	background: #007aff;
	color: #fff;
	font-size: 22upx;
	padding: 5upx 8upx;
	margin-left: 10upx;
	border-radius: 20upx;
	line-height: 24upx;
}
.icon-nv{
	background: #ff698d!important;
}
</style>
