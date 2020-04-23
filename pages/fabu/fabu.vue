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
			<textarea  placeholder="说一句话吧~" v-model="content" />
			<view class="handle-photo">
				<view class="head">
					<upload-image style="width: 100%;" @getSelectImage="selectImage" :images="imageList" />
				</view>
			</view>
		</view>
		<tishikuang ref="openAlert" />
		<comfirm ref="isShow"  @comfirmStatus="isComfirm" />
	</view>
</template> 

<script>
	import uniNavBar from '@/components/uni-nav-bar/uni-nav-bar.vue';
	import uploadImage from '@/components/upload-image.vue';
	import tishikuang from '@/components/tishikuang/tishikuang.vue';
	import comfirm from '@/components/showComfirm/showComfirm.vue';
	export default {
		components:{
			uniNavBar,
			uploadImage,
			tishikuang,
			comfirm
		},
		data(){
			return {
				status:'所有人可见',
				style:'font-size:18px;font-weight: bolder;',
				title: 'choose/previewImage',
				imageList: [],
				content:''
			}
		},
		onShow() {
			let draft = uni.getStorageSync('draft');
			draft.img.length>0? this.imageList = draft.img : this.imageList = [];
			draft.word == ''? this.content = '' : this.content = draft.word;
		},
		mounted(){
			this.$refs.openAlert.show();
		},
		methods:{
			selectImage(argus){
				let {e} = argus;
				this.imageList = e;
			},
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
				if(this.imageList.length>0||this.content != ''){
					this.$refs.isShow.showComfirm('是否保存为草稿？');
					this.flag = true;
				}else{
					uni.clearStorageSync('draft');
					uni.navigateBack({
						delta:1
					});
				}
			},
			isComfirm(e){
				if(e.status){
					uni.setStorageSync('draft',{img:this.imageList,word:this.content});
				}
				uni.navigateBack({
					delta:1
				});
			},
			fabu(){

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
			width: 100%;
			.head{
				width: 100%;
				@include flex_row(space-between);
				.select{
					color: #808080;
				}
			}
		}
	}
</style>
