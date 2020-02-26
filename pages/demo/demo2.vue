<template>
	<view>
		<!-- <view class="box" :class="['bor','fonts']">box</view> -->
		<!-- <view class="box" :class="[age>10?class1:'',sex=='女'?class2:'']">box</view> -->
		<!-- <view class="box" :class="{'bor':isActive,'fonts': isfa}">
			111
		</view> -->
		<!-- <view class="box" :style="{'color':Color,'font-size': size+'px'}">box</view>
	-->
		<!-- <view class="box" v-if="isshow">box</view>
		<button type="primary" @tap="changeShow()">隐藏</button> -->
	<!-- 	<view class="box" v-if="(age>20?'中年人' : '年轻人')">{{age>30?'中年人' : '年轻人'}}</view>
		<button type="primary" @tap="changeAge()">改变年龄</button> -->
		<!-- <view class="box" v-show="isshow">box</view>
		<button type="primary" @tap="changeShow()">隐藏</button> -->
		<!-- <view class="box" v-show="(age>20)">{{age}}</view>
		<button type="default" @tap="changeAge()">隐藏</button> -->
		<template v-if="isshow">
			<view class="box">box</view>
		</template>
		<template v-else>
			<view class="box" style="background: #09BB07;">波形</view>
		</template>
		<button type="primary" @tap="changeShow()">隐藏</button>
	</view> 
</template>

<script>
	export default {
		data() {
			return {
				isshow: true,
				age:10,
				// class1: 'bor',
				// class2: 'fonts',
				// age: 12,
				// sex: "女",
				// isActive: false,
				// isfa: false,
				// Color: '#333',
				// size: 50
			}
		},
		methods: {
			changeShow:function(){
				this.isshow=!this.isshow;
			},
			changeAge:function(){
				this.age+=11
			}
			
		}
	}
	
</script>

<style>
.box{
	background: #09BB07;
	color: #fff;
	font-size: 50upx;
	width: 350upx;
	height: 350upx;
	/* border-radius: 50%; */
	display: flex;
	justify-content: center;
	align-items: center;
}
.bor{
	border: 10upx solid #007AFF;
}
.fonts{
	font-size: 80upx;
	color: red;
}

</style>


