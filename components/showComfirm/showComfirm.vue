<template>
	<view>
		<uni-popup ref="showtip" :type="type" :mask-click="false" @change="change">
			<view class="uni-tip">
				<text class="uni-tip-title">{{title}}</text>
				<text class="uni-tip-content">{{msg}}</text>
				<view class="uni-tip-group-button">
					<text class="uni-tip-button" @click="cancel">取消</text>
					<text class="uni-tip-button" @click="comfirm">确定</text>
				</view>
			</view>
		</uni-popup>
	</view>
</template>

<script>
	import uniPopup from '@/components/showComfirm/uni-popup.vue'; 
	export default {
		components:{
			uniPopup
		},
		data() {
			return {
				type:'center',
				msg:'',
				title:'提示'
			};
		}, 
		methods:{
			showComfirm(msg,title) {
				this.msg = msg? msg:'';
				this.title = title? title: '提示';
				this.$refs.showtip.open();
			},
			comfirm(){
				// console.log(this.$refs.showtip)
				this.$refs.showtip.close();
				this.$emit('comfirmStatus',{status:true});
				// console.log(this.$refs.showtip)
				// return
			},
			cancel() {
				this.$refs.showtip.close();
				this.$emit('comfirmStatus',{status:false});
				// this.$refs.showtip.close();
			},
			change(e) {
				// console.log('是否打开:' + e.show)
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
    
    	.uni-tip-title {
    		margin-bottom: 10px;
    		text-align: center;
    		font-weight: bold;
    		font-size: 16px;
    		color: #333;
    	}
    
    	.uni-tip-content {
    		/* padding: 15px;
    */
    		font-size: 14px;
    		color: #666;
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
    		color: #3b4144;
    	}
</style>
