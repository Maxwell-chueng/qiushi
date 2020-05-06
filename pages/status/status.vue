<template>
	<view>
         <uni-nav-bar :statusBar="true" class="nav">
			 <block slot="left">
				 <view class="nav-left">
				     <text class="iconfont">&#xe609;</text>
				 </view>
			 </block>
			 <view class="center">
			 	<view @click="handleCate(0)" :class="{active:currentIndex === 0}">关注</view>
			 	<view @click="handleCate(1)" :class="{active:currentIndex === 1}">话题</view>
			 </view>
			 <block slot="right">
				 <view class="nav-right">
				     <text  class="iconfont">&#xe653;</text>
				 </view>
			 </block>
		</uni-nav-bar>
	</view>
</template>

<script>
	import uniNavBar from "../../components/uni-nav-bar/uni-nav-bar.vue";
	export default {
		components:{
			uniNavBar
		},
		data() {
			return {
				currentIndex:0
			};
		},
		methods:{
			handleCate(index){
				this.currentIndex = index;
			}
		}
	}
</script>

<style lang="scss" scoped>
	.nav-left,.nav-right{
		width: 50upx;
		text{
			font-size: 40upx;
			color: #FF9A22;
		}
	}
	.nav-left{
		width: 0%;
		margin-left: 16upx;
	}
	.nav-right{
		width: 0%;
		// margin-right: -22upx;
		text{
		    color: #000;	
		}
	}
	.center{
		width: 100%;
		@include flex_row();
		margin-right: 20upx;
		view{
			margin: 0 20upx;
			border-bottom: 4upx solid rgba(255,255,255,0);
		}
	}
	.active{
		border-bottom: 4upx solid #FEDE33 !important;
		border-radius: 4upx;
	}
</style>
