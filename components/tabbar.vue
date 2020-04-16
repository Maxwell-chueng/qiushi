<template>
	<view class="tabbar">
			<scroll-view scroll-x="true" class="list">
				<block v-for="(list,index) in arr" :key="list.id">
				    <view class="item">{{list.name}}</view>
				</block>
			</scroll-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				arr:[{
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
				}]
			};
		}
	}
</script>

<style scoped lang="scss">
</style>
