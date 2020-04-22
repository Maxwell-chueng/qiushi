<template>
	<view class="upload-image">
		<view class="uni-list list-pd">
			<view class="uni-list-cell cell-pd">
				<view class="uni-uploader">
					<view class="uni-uploader-head">
						<view class="uni-uploader-title">点击可预览选好的图片</view>
						<view class="uni-uploader-info">{{imageList.length}}/9</view>
					</view>
					<view class="uni-uploader-body">
						<view class="uni-uploader__files">
							<block v-for="(image,index) in imageList" :key="index">
								<view class="uni-uploader__file">
									<text class="iconfont lajitong" @click="deleteSomneOne(index)">&#xe605;</text>
									<image class="uni-uploader__img" :src="image" :data-src="image" @tap="previewImage"></image>
								</view>
							</block>
							<view class="uni-uploader__input-box">
								<view class="uni-uploader__input" @tap="chooseImage"></view>
							</view>
						</view>
					</view>
				</view>
			</view>
		</view>
		<showComfirm ref="comfirm" @comfirmStatus ="comfirmDelete" />
		<showModal ref="notice" />
	</view>
</template>

<script>
	let sourceType = [
		['camera'],
		['album'],
		['camera', 'album']
	]
	let sizeType = [
		['compressed'],
		['original'],
		['compressed', 'original']
	]
	import showComfirm from '@/components/showComfirm/showComfirm.vue';
	import showModal from '@/components/showModal/showModal.vue'
	export default {
		components:{
			showComfirm,
			showModal
		},
		data() {
			return {
				title: 'choose/previewImage',
				imageList: [],
				sourceTypeIndex: 2,
				sourceType: ['拍照', '相册', '拍照或相册'],
				sizeTypeIndex: 2,
				sizeType: ['压缩', '原图', '压缩或原图'],
				countIndex: 8,
				count: [1, 2, 3, 4, 5, 6, 7, 8, 9]	
			};
		},
		watch:{
			imageList(e){
				this.$emit('getSelectImage',{e});
			}
		},
		methods:{
			comfirmDelete(e){
			    let {status} = e;
				if(status){
				    this.imageList.splice(this.deleteIndex,1);
				}else{
					return;
				}
			},
			deleteSomneOne(index){
				this.deleteIndex = index;
				this.$refs.comfirm.showComfirm('确认删除该图片？');
			},
			async chooseImage() {
				// #ifdef APP-PLUS
				// TODO 选择相机或相册时 需要弹出actionsheet，目前无法获得是相机还是相册，在失败回调中处理
				if (this.sourceTypeIndex !== 2) {
					let status = await this.checkPermission();
					if (status !== 1) {
						return;
					}
				}
				// #endif
			
				if (this.imageList.length === 9) {
					this.$refs.notice.showMsg({msg:'最多上传9张图片',status:'error'});
					return
				}
				uni.chooseImage({
					sourceType: sourceType[this.sourceTypeIndex],
					sizeType: sizeType[this.sizeTypeIndex],
					count: this.imageList.length + this.count[this.countIndex] > 9 ? 9 - this.imageList.length : this.count[this.countIndex],
					success: (res) => {
						this.imageList = this.imageList.concat(res.tempFilePaths);
					},
					fail: (err) => {
						// #ifdef APP-PLUS
						if (err['code'] && err.code !== 0 && this.sourceTypeIndex === 2) {
							this.checkPermission(err.code);
						}
						// #endif
						// #ifdef MP
						uni.getSetting({
							success: (res) => {
								let authStatus = false;
								switch (this.sourceTypeIndex) {
									case 0:
										authStatus = res.authSetting['scope.camera'];
										break;
									case 1:
										authStatus = res.authSetting['scope.album'];
										break;
									case 2:
										authStatus = res.authSetting['scope.album'] && res.authSetting['scope.camera'];
										break;
									default:
										break;
								}
								if (!authStatus) {
									uni.showModal({
										title: '授权失败',
										content: 'Hello uni-app需要从您的相机或相册获取图片，请在设置界面打开相关权限',
										success: (res) => {
											if (res.confirm) {
												uni.openSetting()
											}
										}
									})
								}
							}
						})
						// #endif
					}
				})
			},
			previewImage(e){
				var current = e.target.dataset.src
				uni.previewImage({
					current: current,
					urls: this.imageList
				})
			},
		}
	}
</script>

<style lang="scss" scoped>
    .uni-uploader__file{
    	position: relative;
    	.lajitong{
    		position: absolute;
    		width: 40upx;
    		height: 40upx;
    		top: 0;
    		right: 0;
    		background-color: #fafafa;
    		color: #000;
    		@include flex_row();
    		z-index: 10;
    	}
    }
	.uni-list::before{
		content: '';
		height: 0;
	}
	.uni-list::after{
		content: '';
		height: 0;
	}
	.list-pd {
		margin-top: 50rpx;
	}
	.upload-image{
		width: 100%;
		.uni-list{
			width: 100%;
		}
	}
</style>
