<template>
	<view class="index">
		<view class="nav">
			<tabbar :tab="tab" :currentIndex="currentIndex" :distance="distance" @tapTab="Handletab" />
		</view>
		<view class="swiper"> 
	<!-- swiper中嵌套scrollView可以实现页面既可上下拉动，又可左右滚动的效果 -->
	<!-- 上下拉动是scrollView的效果，左右滑动是swiper的效果，与轮播图类似 -->
	<!-- 需要根据官方提供的接口获取设备的可用高度，再减去tabbar的高度得到swpier的高度和scroll-view的高度 -->
	<!-- :current 可以动态设置轮播图的页数，点击上面的tabbar促使currentIndex发生更改，造成下面的轮播图页数发生改变，所以就有点击tabbar页面滚动的效果 -->
	<!-- @change当轮播图的页数被滑动时能够获取当前的页数，在change 的回调函数中修改currentIndex使得，上面tababr 的index也发生了变化 -->
			<swiper @change="changeSwiper" :style="{height:canUseHeight+'px'}" :current="currentIndex">
				<swiper-item v-for="(item,index) in arr" :key="index">
					<scroll-view scroll-y="true" :style="{height:canUseHeight+'px'}">
						<view class="" v-if="item.list.length>0">
							<block v-for="(list,i) in item.list" :key="i">
								<indexComp :item="list" :index="i" @deletSomeOne="deleteArtist" />
							</block>														
						</view>
						<view class="" v-else>
							<image class="defaultImg" src="../../static/image/nothing.png" mode="widthFix"></image>
						</view>
					</scroll-view>
				</swiper-item>
			</swiper>
		</view>
		<showModal ref="notice" /> 
	</view>
</template>

<script>
	import indexComp from '../../components/index-comp.vue';
	import tabbar from '../../components/tabbar.vue';
	import showModal from "@/components/showModal.vue";
	export default {
		components:{
			indexComp,
			tabbar,
			showModal
		},
		data() {
			return {
				canUseHeight:500,
				currentIndex:0,
				distance:0,
				tab:[{
						id:0,
						name:'关注'
					},{
						id:1,
						name:'推荐'
					},{
						id:2,
						name:'体育'
					},{
						id:3,
						name:'热点'
					},{
						id:4,
						name:'财经'
					},{
						id:5,
						name:'娱乐'
					},{
						id:6,
						name:'军事'
					},{
						id:7,
						name:'历史'
					}],
				// status为0时,表示没有操作,1为顶,2为踩
				arr:[{
					list:[

					]
				},{
					list:[
						{
							name:"哲学家",
							photo:'../../static/image/demo6.jpg',
							guanzhu:1,
							title:'如何用手账改变你的一生',
							contentImage:"../../static/image/datapic/37.jpg",
							type:'video',
							info:{
								status:2, 
								top:10,
								down:2
							},
							videoInfo:{
								time:'2:47',
								play:304
							},
							comment:999,
							share:777
						}
					]
				},{
					list:[
						{
							name:"哲学家",
							photo:'../../static/image/demo6.jpg',
							guanzhu:0,
							title:'如何用手账改变你的一生',
							type:'image',
							contentImage:"../../static/image/datapic/37.jpg",
							info:{
								status:1,
								top:12,
								down:0
							},
							comment:999,
							share:777
						},{
							name:"哲学家",
							photo:'../../static/image/demo6.jpg',
							guanzhu:1,
							title:'如何用手账改变你的一生',
							contentImage:"../../static/image/datapic/37.jpg",
							type:'video',
							info:{
								status:2, 
								top:10,
								down:2
							},
							videoInfo:{
								time:'2:47',
								play:304
							},
							comment:999,
							share:777
						}
					]
				},{
					list:[
						{
							name:"哲学家",
							photo:'../../static/image/demo6.jpg',
							guanzhu:0,
							title:'如何用手账改变你的一生',
							type:'image',
							contentImage:"../../static/image/datapic/37.jpg",
							info:{
								status:1,
								top:12,
								down:0
							},
							comment:999,
							share:777
						}
					]
				},{
					list:[
						{
							name:"哲学家",
							photo:'../../static/image/demo6.jpg',
							guanzhu:0,
							title:'如何用手账改变你的一生',
							type:'image',
							contentImage:"../../static/image/datapic/37.jpg",
							info:{
								status:1,
								top:12,
								down:0
							},
							comment:999,
							share:777
						},{
							name:"哲学家",
							photo:'../../static/image/demo6.jpg',
							guanzhu:1,
							title:'如何用手账改变你的一生',
							contentImage:"../../static/image/datapic/37.jpg",
							type:'video',
							info:{
								status:2, 
								top:10,
								down:2
							},
							videoInfo:{
								time:'2:47',
								play:304
							},
							comment:999,
							share:777
						}
					]
				},{
					list:[
						{
							name:"哲学家",
							photo:'../../static/image/demo6.jpg',
							guanzhu:1,
							title:'如何用手账改变你的一生',
							contentImage:"../../static/image/datapic/37.jpg",
							type:'video',
							info:{
								status:2, 
								top:10,
								down:2
							},
							videoInfo:{
								time:'2:47',
								play:304
							},
							comment:999,
							share:777
						}
					]
				},{
					list:[
						{
							name:"哲学家",
							photo:'../../static/image/demo6.jpg',
							guanzhu:0,
							title:'如何用手账改变你的一生',
							type:'image',
							contentImage:"../../static/image/datapic/37.jpg",
							info:{
								status:1,
								top:12,
								down:0
							},
							comment:999,
							share:777
						},{
							name:"哲学家",
							photo:'../../static/image/demo6.jpg',
							guanzhu:1,
							title:'如何用手账改变你的一生',
							contentImage:"../../static/image/datapic/37.jpg",
							type:'video',
							info:{
								status:2, 
								top:10,
								down:2
							},
							videoInfo:{
								time:'2:47',
								play:304
							},
							comment:999,
							share:777
						}
					]
				},{
					list:[
						{
							name:"哲学家",
							photo:'../../static/image/demo6.jpg',
							guanzhu:0,
							title:'如何用手账改变你的一生',
							type:'image',
							contentImage:"../../static/image/datapic/37.jpg",
							info:{
								status:1,
								top:12,
								down:0
							},
							comment:999,
							share:777
						}
					]
				}]
			}
		},
		onLoad() {
            this.getIndexCompHeight();
		},
		onNavigationBarSearchInputClicked(){
			uni.navigateTo({
				url:'/pages/search/search'
			})
		},
		watch:{
			// 监听currentIndex,索引大于3式,动态设置tabbar横向滚动条的滚动距离
			currentIndex(i){
				if(i>3){
					this.distance = i *100;
				}else{
					this.distance = 0;
				}
			}
		},
		methods: {
			deleteArtist(e){
				let {index} = e;
				this.$refs.notice.showMsg({msg:'删除成功',time:1000}).then(()=>{
				    this.arr[this.currentIndex].list.splice(index,1);
				}) 
			},
            Handletab(e){
				this.currentIndex =  e.i;
			},
			// 当swpier发生滚动时,改变currentIndex促使tabbar也发生变化
			changeSwiper(e){
				this.currentIndex =  e.detail.current;
			},
			// 获取设备的可用屏幕高度
			getIndexCompHeight(){
				uni.getSystemInfo({
					success:(e)=>{
						this.canUseHeight =  e.windowHeight - uni.upx2px(80);
					}
				})
			}
		}
	}
</script>

<style scoped lang="scss">
    .defaultImg{
		width: 400upx;
		height: 600upx;
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%,-50%); 
	}
</style>
