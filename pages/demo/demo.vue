<template>
	<view>
		<view class="font">
			{{zhweight}}
		</view>
	</view>
</template>

<script>
	export default{
		data() {
			return {
				weight: 13200
			}
		},
		computed:{
			zhweight:function(){
				return this.weight>1000? (this.weight/1000)+ 'kg':this.weight+'g'
			}
		},
		methods:{
			
		}
	}
</script>

<style>
	.font{
		font-size: 50upx;
	}
</style>
