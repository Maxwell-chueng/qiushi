<template>
	<view class="index">
		<view class="nav">
			<block v-for="(item,index) in arr" :key="index">
			     <indexComp :item="item" :index="index" />
			</block>
		</view>
	</view>
</template>

<script>
	import indexComp from '../../components/index-comp.vue';
	export default {
		components:{
			indexComp
		},
		data() {
			return {
				// status为0时,表示没有操作,1为顶,2为踩
				arr:[{
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
				}]
			}
		},
		onLoad() {

		},
		methods: {

		}
	}
</script>

<style scoped lang="scss">

</style>
