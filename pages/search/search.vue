<template>
	<view>
		<uniNavBar statusBar="true">
			<view class="search-center">
				<input type="text" placeholder="搜索糗事" v-model='searchContent' />
				<view class="iconfont fangdajing">
					&#xe606;
				</view>
			</view>
			<block slot="right">
				<view class="search-right">
					<text v-show="hasString" @click="goBack">取消</text>
					<text v-show="!hasString" @click="goSearch">搜索</text>
				</view>
			</block>
		</uniNavBar>
	    <showModal ref="notice" />	
	</view>
</template>

<script>
	import showModal from "@/components/showModal/showModal.vue";
    import uniNavBar from '@/components/uni-nav-bar/uni-nav-bar.vue'
	export default {
		components:{
			showModal,
			uniNavBar
		},
		data() {
			return {
				searchContent:'',
				defaultIconShow:true,
				hasString:true
			}
		},
		watch:{
			searchContent(e){
				e ? this.hasString = false : this.hasString = true;
			}
		},
		methods: {
			goBack(){
				uni.navigateBack({
					delta:1
				})
			},
			goSearch(){
				console.log('search');
			}
		}
	}
</script>

<style scoped lang="scss">
	.search-center{
		width: 80vw;
			position: absolute;
			left: 30upx;
		input{
			text-align: left;
			font-size: 24upx;
			height: 44upx;
			background-color: rgba(0,0,0,0.1);
		    border-radius: 10upx;
			z-index: 998;
			box-sizing: border-box;
			padding-left: 50upx;
		}
		.fangdajing{
			position: absolute;
			left: 10upx;
			top: 6%;
			font-size: 22upx;
			z-index: 999;
		}
	}
</style>
