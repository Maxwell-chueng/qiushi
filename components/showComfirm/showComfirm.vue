<template>
	<view>
		<uni-popup ref="showtip" :type="type" :mask-click="false" @change="change">
			<view class="uni-tip">
				<text class="uni-tip-title">{{title}}</text>
				<text class="uni-tip-content">{{msg}}</text>
				<view class="uni-tip-group-button">
					<text class="uni-tip-button" @click="cancel('tip')">取消</text>
					<text class="uni-tip-button" @click="comfirm('tip')">确定</text>
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
			showComfirm(msg,title,type='center', open='tip') {
				this.msg = msg? msg:'';
				this.title = title? title: '提示';
				switch (type) {
					case 'top':
						this.content = '顶部弹出 popup'
						break
			
					case 'bottom':
						this.content = '底部弹出 popup'
						break
					case 'center':
						this.content = '居中弹出 popup'
						break
				}
				this.type = type
				this.$nextTick(() => {
					this.$refs['show' + open].open()
				})
			},
			comfirm(type){
				this.$emit('comfirmStatus',{status:true});
				this.$refs['show' + type].close();
			},
			cancel(type) {
				this.$emit('comfirmStatus',{status:false});
				this.$refs['show' + type].close();
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
