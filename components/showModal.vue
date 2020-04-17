<template>
	<view>
		<uniPopup type="center" ref="popup" :maskClick="false" >
            <view class="content">
            	<text v-if="status == 'success'" class="iconfont success">&#xe679;</text>
            	<text v-else class="iconfont fail">&#xe67f;</text>
            	<text >{{msg}}</text> 
            </view>
		</uniPopup>
	</view>
</template>

<script>
	import uniPopup from "@/components/uni-popup/uni-popup.vue";
	export default {
		components:{
			uniPopup
		},
		data() {
			return {
				msg:'操作成功',
				status:'success',
				isShow:false
			}
		},
		methods:{
			showMsg(option){
				option? option : option = {};
				option.msg? option.msg : option.msg = '操作成功';
				option.time? option.time : option.time = 1500;
				option.delay? option.delay : option.delay = 0;
				option.status? option.status : option.status = 'success';
				console.log('[notice]',option);
				return  new Promise((resolve,reject)=>{
					this.msg = option.msg;
					this.status = option.status;
					setTimeout(()=>{
							this.$refs.popup.open();
						setTimeout(()=>{
								this.$refs.popup.close();
								return resolve();	
						},option.time);
					},option.delay);
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
    .success{
		width: 40upx;
		height: 40upx;
		color: #1afa29;
		line-height:40upx;
	}
    .fail{
		width: 40upx;
		height: 40upx;
		color: #d81e06;
		line-height:40upx;
	}
	.content{
		@include flex_row();
		width: 100%;
		@include box_size(20upx,20upx);
		height: 80upx;
		background-color: #fff;
		color: #000; 
		box-shadow: 0upx 10upx 20upx 1upx rgba(0,0,0,.1);
	}
</style>
