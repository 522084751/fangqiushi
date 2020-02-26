<template>
	<view class="">
		<!-- <view class="font">
			{{name}}
		</view>
		<view class="box" @tap="clickevent()">按钮</view> -->
		<view class="box1" @tap.stop="box1event()">
			外面
			<view class="box2" @tap.stop="box2event()">里面</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				name:'hahaha'
			}
		},
		methods:{
			clickevent: function(){
				this.name="xixixi"
				console.log(this.name)
			},
			box1event: function(){
				console.log("点击了外面")
			},
			box2event: function(){
				console.log("点击了里面")
			}
		}
	}
</script>

<style>
.box1{
	width: 100%;
	height: 500upx;
	background: #09BB07;
	color: #fff;
	font-size: 40upx;
	display: flex;
	justify-content: center;
	align-items: center;
}
.box2{
	width: 300upx;
	height: 300upx;
	background: #576B95;
	color: #fff;
	font-size: 40upx;
	display: flex;
	justify-content: center;
	align-items: center;
}
.box{
	background: #09BB07;
	color: #fff;
	width: 80%;
	margin: auto;
	height: 80upx;
	font-size: 50upx;
	border-radius: 8upx;
	border: 1px solid #eee;
	display: flex;
	justify-content: center;
	align-items: center;
}
.font{
	font-size: 50upx;
	border: 1upx solid #ccc;
	padding: 20upx;
}
</style>
