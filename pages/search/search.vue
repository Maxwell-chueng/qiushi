<template>
	<view>
	    <showModal ref="notice" />	
	</view>
</template>

<script>
	import showModal from "@/components/showModal/showModal.vue";
	export default {
		components:{
			showModal
		},
		data() {
			return {
				searchContent:''
			}
		},
		onNavigationBarButtonTap(e){
			if(e.index === 0){
				uni.navigateBack({
					delta:1
				})
			}
		},
		onNavigationBarSearchInputChanged(e){
			console.log(JSON.stringify(e));
			let {text} = e;
			this.searchContent = text;
		},
		onNavigationBarSearchInputConfirmed(){
			let text = this.searchContent;
			if(text.replace(/(^\s*)|(\s*$)/g, "")){
				console.log('发送请求');
			}else{ 
				this.$refs.notice.showMsg({msg:'搜索内容不能为空',status:'error'});
			}
		},
		methods: {
			
		}
	}
</script>

<style>

</style>
