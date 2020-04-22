<template>
		<view class="list">
			<view class="item animated fadeInRight fast">
				<view class="head container"> 
                    <view class="avatar">
                    	<image :src="newList.photo"/> 
                    	<text class="name">{{newList.name}}</text> 
                    </view>
					<view class="foucs">
						<view v-show="newList.guanzhu == 0" class="contents" @click="joinFoucs">
							<view class="iconfont btn fl" >
								&#xe684; 关注
							</view>							
						</view>
						<text class="iconfont close fr" @click="deleteArtist">&#xe6aa;</text>
					</view>
				</view>
				<view class="content container">
					<view class="title">
						{{newList.title}}
					</view>
					<image :src="newList.contentImage"/>
					<text class="iconfont start" v-if="newList.type === 'video'">&#xe6ac;</text>
					<view class="video-info" v-if="newList.type === 'video'">
					    <text>{{newList.videoInfo.play}}</text>
						<text>次播放</text>
						<text>{{newList.videoInfo.time}}</text>
					</view>
				</view>
				<view class="footer container">
                    <view class="fl">
                    	<view @click="operation('top')" :class="[newList.info.status == 1?'active':'']"> 
                    		<text class="iconfont">&#xe64e;</text>
                    		<text>{{newList.info.top}}</text>
                    	</view>
                    	<view @click="operation('down')" :class="[newList.info.status == 2? 'active':'']">
                    		<text class="iconfont">&#xe600;</text>
                    		<text>{{newList.info.down}}</text>
                    	</view> 
                    </view>
					<view class="fr">
						<view>
							<text class="iconfont">&#xeb97;</text>
							<text>{{item.comment}}</text>
						</view>
						<view>
							<text class="iconfont">&#xe627;</text>
							<text>{{item.share}}</text>
						</view>
					</view>
				</view>
			</view>
			<showModal ref="notice" />
		</view>
</template>

<script>
	import showModal from "@/components/showModal/showModal.vue";
	export default {
		components:{
			showModal
		},
		props:{
			item:{
				type:Object,
				default:function(){
					return {};
				}
			},
			index:{
				type:Number,
				default:0
			}
			
		},
		data() {
			return {
				newList:{} 
			};
		},
		created(){
			this.newList = this.item;
		},
		methods:{
			// 删除文章
			deleteArtist(){
				this.$emit('deletSomeOne',this.index);
			},
			// 关注                             
			joinFoucs(){
				this.newList.guanzhu = 1;
				this.$refs.notice.showMsg({msg:'关注成功'});
			},
			operation(type){
					switch(type){
						case 'top' :
						// console.log(11);
	                        if(this.newList.info.status === 1){return};
							this.newList.info.top ++ ;
							if(this.newList.info.status === 2){
								this.newList.info.down -- ;
							}
							this.newList.info.status = 1;
							break;
						case 'down' :
						// console.log(22);
	                        if(this.newList.info.status === 2){return};
							this.newList.info.down ++ ;
							if(this.newList.info.status === 1){
								this.newList.info.top -- ;
							}
							this.newList.info.status = 2;
							break;
					}		
				}
			}
	}
</script>

<style scoped lang="scss">
	.fl{
		float: left;
	}
	.fr{
		float: right;
	}
    .container{
    	@include box_size(0upx,20upx);
    }
    .item{
    	@include flex_column();
    }
    .head{
    	width: 100%;
    	@include flex_row(space-between);
		@include box_size(16upx,20upx);
    	.avatar{
    	    @include flex_row(space-between);	
    	}
    	.avatar{
    		color: #CCCCCC; 
    		.name{
    			margin-left: 16upx;
    		}
    	}
    	.foucs{
			display: flex;
			justify-content: flex-end;
			align-items: center;
			flex-direction: row;
    		width: 150upx;
    		height: 50upx;
			.contents{
				overflow: hidden;
			}
    	}
    	.btn{
    		font-size: 24upx;
    		border-radius: 4upx;
    		background-color: #f7f7f7;
    		width: 100upx; 
    		height: 50upx;
    		@include flex_row();
    	}
    	.close{
    		width: 40upx;
    		font-size: 24upx;
    		color: #D5D5D5;
    		font-weight: bolder;
    		@include flex_row();
    	}
    	image{
    		width: 90upx;
    		height: 90upx;
    		border-radius: 50%;
    	}
    }
    .content{
    	width: 100%;
    	position: relative;
    	.title{
    		font-size: 36upx;
    		@include box_size(8upx,0);
    	}
    	image{
    		width: 100%;
    		height: 380upx;
    		border-radius: 6upx;
    	}
    	.start{
    		position: absolute;
    		top: 50%;
    		left: 50%;
    		transform: translate(-50%,-40%); 
    		color: #fff; 
    		font-size: 150upx;
    	}
    	.video-info{
    		position: absolute;
    		bottom: 30upx;
    		right: 30upx;
    		border-radius: 20upx;
    		padding: 0 20upx;
    		background-color: rgba(0,0,0,.3);
    		color: #fff;
    	}
    	.video-info>text{
    		margin-right: 10upx;
    	}
    }
    .footer{
    	width: 100%;
    	@include flex_row(space-between);
    	@include box_size(16upx,16upx);
    	border-bottom: 3upx solid #f0f0f0;
    }
    .footer>view{
    	color: #D5D5D5;
    	@include flex_row(space-between);
    	width: 200upx;
    	view{
    		flex: 1;
    		@include flex_row(space-around);
    	}
    }
	.active{
		color: #FEE42A;
	}
</style>
