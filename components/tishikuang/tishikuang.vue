<template>
	<view>
		<uni-popup ref="isShow" :mask-click="false" >
			<view class="uni-tip">
				<view class="img">
					<image src="../../static/image/addinput.png" mode="widthFix"></image>
				</view>
				<text class="uni-tip-content">1、涉及黄色，政治，广告及骚扰信息</text>
				<text class="uni-tip-content">2、涉及人身攻击</text>
				<text class="uni-tip-content">3、留联系方式、透露他人隐私</text>
				<text class="uni-tip-content">一经核实将被封禁、情节严重者永久封禁</text>
				<view class="uni-tip-group-button">
					<text class="uni-tip-button" @click="comfirm">朕知道了</text>
				</view>
			</view>
		</uni-popup>
	</view>
</template>
<script>
	import uniPopup from "@/components/tishikuang/uni-popup.vue";
	export default {
		components:{
			uniPopup
		},
		data() {
			return {
				
			};
		},
        methods:{
			show(){
				this.$refs.isShow.open();
			},
			comfirm(){
				this.$refs.isShow.close();
			}
		}
	}
</script>

<style lang="scss" scoped>
    .uni-tip {
    	    text-align: center;
    		/* #ifndef APP-NVUE */
    		display: flex;
    		flex-direction: column;
    		/* #endif */
    		padding: 15px;
    		width: 300px;
    		background-color: #fff;
    		border-radius: 10px;
    	}
    .img{
		width: 100%;
		@include flex_row();
		image{
			width: 60%;
		}
	}
    	.uni-tip-title {
    		margin-bottom: 10px;
    		text-align: center;
    		font-weight: bold;
    		font-size: 16px;
    		color: #F2B94A;
    	}
    
    	.uni-tip-content {
    		/* padding: 15px;
    */
    		font-size: 14px;
    		color: #000;
			@include flex_row(flex-start);
    	}
    
    	.uni-tip-group-button {
    		/* #ifndef APP-NVUE */
    		display: flex;
    		/* #endif */
    		flex-direction: row;
    		margin-top: 20px;
    	}
    
    	.uni-tip-button {
    		flex: 1;
    		text-align: center;
    		font-size: 14px;
    		color: #000;
			background-color: #FFE934;
			font-size: 32upx;
			height: 70upx;
			border-radius: 10upx;
			@include flex_row();
    	}
</style>
