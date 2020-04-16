<template>
	<view class="tabbar">
        <view class="list">
			<scroll-view scroll-x="true" class="scroll" :scroll-left="distance" @scroll="scroll">
				<block v-for="(list,index) in tab" :key="list.id">
					<view class="item" :class="{active:currentIndex === index}" @click="switchTab(index)">{{list.name}}</view>
				</block>
			</scroll-view>
        </view>
	</view>
</template>

<script>
	export default {
		props:{
			tab:{
				type:Array,
				default:function(){
					return {}
				}
			},
			currentIndex:{
				type:Number,
				default:0
			},
			distance:{
				type:Number,
				default:0
			}
		},
		data() {
			return {
				old:{
					scrollTop:0
				}
		    }
		},
		methods:{
			scroll(e){
				this.old.scrollTop = e.detail.scrollTop;
			},
			switchTab(i){
				this.$emit('tapTab',{i})
			}
		}
	}
</script>

<style scoped lang="scss">
	.tabbar{
		width: 100%;
		height: 80upx;
			.list{
				height: 80upx;
				@include flex_row();
				.scroll{
					width: 100%;
					overflow: hidden;
					white-space: nowrap;
					.item{
						flex: 1;
						display: inline-block;
						height: 100%;
						// line-height: 28upx;
						margin: 0 41upx;
						color: #969696;
						font-weight: bold;
					}
		     	}
	      	}
	}
	.active{
		border-bottom: 6upx solid #FEE42A;
		border-radius: 4upx;
		color: #000!important;
	}
</style>
