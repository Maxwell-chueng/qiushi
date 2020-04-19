<template>
	<view>
        <view class="nav">
        	<!-- ：statusbar属性为true使用uni-app自带的状态栏 -->
        	<uni-nav-bar :statusBar="true" left-icon="arrowleft" right-text="发布" @clickLeft="back" @clickRight="fabu" 
			:rightTextStyle="style">
        	    <view class="nav-content" @click="switchPrivate">
        	    	<text>{{status}}</text>
        	    	<text class="iconfont ">&#xe60e;</text>
        	    </view>
        	</uni-nav-bar>
        </view>
		<view class="content container">
			<textarea  placeholder="说一句话吧~" />
			<view class="handle-photo">
				<view class="head">
					<text>点击可预览选好的图片</text>
					<text class="select"> 0/9</text>
				</view>
			</view>
		</view>
	</view>
</template> 

<script>
	import uniNavBar from '@/components/uni-nav-bar/uni-nav-bar.vue'
	export default {
		components:{
			uniNavBar,	
		},
		data() { 
			return {
				status:'所有人可见',
				style:'font-size:18px;font-weight: bolder;'
			};
		},
		methods:{
			switchPrivate(){
				let itemList = ['所有人可见', '仅自己可见'];
				// uni-app自带的交互多选框
				uni.showActionSheet({
					itemList,
				    success:(res)=>{
						this.status = itemList[res.tapIndex];
						console.log(this.status);
				    }
				}); 
			},
			back(){
				uni.navigateBack({
					delta:1
				});
			},
			fabu(){
				console.log('发布');
			}
		}
	}
</script>

<style lang="scss" scoped>
	.container{
		@include box_size(0,20upx);
	}
    .nav-content{
		width: 100%;
		@include  flex_row();
	}
	.content{
		textarea{
			width: 100%;
		    // border: 2upx solid #000;
			@include box_size(20upx,0);
			color: #808080;
		}
		.handle-photo{
			.head{
				@include flex_row(space-between);
				.select{
					color: #808080;
				}
			}
		}
	}
</style>
