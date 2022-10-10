<template>
	<view class="container">
		<preview-image ref="previewImage" :imgs="imgList" :baseUrl="baseUrl" :saveBtn="false" :rotateBtn="circular"></preview-image>
		<view class="top">
			<view class="top_inner">
				<view class="top_left">
					<image :src="baseUrl+info.iconSrc" class="top_img" @click="imgPreview('icon')"></image>
				</view>
				<view class="top_right">
					<view class="text1">
						<view class="name">{{info.name}}</view>
						<view class="level">{{info.level}}</view>
					</view>
					<view class="text2">
						<view class="address text3">{{info.address}}</view>
						<view class="age text3">{{info.age}}</view>
						<view class="years ">{{info.years}}</view>
					</view>
				</view>
			</view>
		</view>
		<view class="cneter">
			<view class="flex info_block">
				<view class="info_content">
					<view class="info_content_left">类&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;型：</view>
					<view class="info_content_right">{{info.type}}</view>
				</view>
			</view>
			<view class="info_title">基本信息</view>
			<view class="flex info_block">
				<view class="info_content">
					<view class="info_content_left">学&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;历：</view>
					<view class="info_content_right">{{info.education}}</view>
				</view>&nbsp;
				<view class="info_content">
					<view class="info_content_left">民&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;族：</view>
					<view class="info_content_right">{{info.nation}}</view>
				</view>
				<view class="info_content">
					<view class="info_content_left">属&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;相：</view>
					<view class="info_content_right">{{info.zodiac}}</view>
				</view>
				<view class="info_content">
					<view class="info_content_left">星&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;座：</view>
					<view class="info_content_right">{{info.constellation}}</view>
				</view>
				<view class="info_content">
					<view class="info_content_left">身&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;高：</view>
					<view class="info_content_right">{{info.height}}</view>
				</view>
				<view class="info_content">
					<view class="info_content_left">体&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;重：</view>
					<view class="info_content_right">{{info.weight}}</view>
				</view>
				<view class="info_content">
					<view class="info_content_left">性&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;别：</view>
					<view class="info_content_right">{{info.gender}}</view>
				</view>
				<view class="info_content">
					<view class="info_content_left">婚姻状况：</view>
					<view class="info_content_right">{{info.marital}}</view>
				</view>
				<view class="info_content">
					<view class="info_content_left">语&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;言：</view>
					<view class="info_content_right">{{info.language}}</view>
				</view>
				<view class="info_content">
					<view class="info_content_left">住家情况：</view>
					<view class="info_content_right">{{info.home}}</view>
				</view>
				<view class="info_content">
					<view class="info_content_left">自我介绍：</view>
					<view class="info_content_right">{{info.introduce}}</view>
				</view>
				<view class="info_content">
					<view class="info_content_left">专业技能：</view>
					<view class="info_content_right">{{info.skill}}</view>
				</view>
			</view>
			<view class="info_title">工作生活照</view>
			<view class="img_info">
				<image v-for="(item,index) in lifePhotoList" :key="index" :src="baseUrl+item" class="photo" mode="aspectFill" @click="imgPreview(lifePhotoList,index)"></image>
			</view>
			<view class="info_title">资格证照片</view>
			<view class="img_info">
				<image v-for="(item,index) in certificationPhotoList" :key="index" :src="baseUrl+item" class="photo" mode="aspectFill" @click="imgPreview(certificationPhotoList,index)"></image>
			</view>
			<view class="info_title">月子餐照片</view>
			<view class="img_info">
				<image v-for="(item,index) in mealPhotoList" :key="index" :src="baseUrl+item" class="photo" mode="aspectFill" @click="imgPreview(mealPhotoList,index)"></image>
			</view>
			<view class="info_title">工作经历</view>
			<view class="info_block">
				<view v-for="(item,index) in workExperience" :key="index" class="work">
					<view class="work_timeq"><view class="dot"></view>{{item.timeq}}</view>
					<view class="work_info">{{item.work}}</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import config from '@/config/config.js';
	import data from '@/config/data.js';
	import previewImage from '@/components/kxj-previewImage/kxj-previewImage.vue';
	export default {
		components:{previewImage},
		data() {
			return {
				baseUrl:config,
				//基本信息
				info:data.info,
				//生活照
				lifePhotoList:data.lifePhotoList,
				//资格证照片
				certificationPhotoList:data.certificationPhotoList,
				//月子餐照片
				mealPhotoList:data.mealPhotoList,
				//工作经历
				workExperience:data.workExperience,
				//预览图片数组
				imgList:[],
				//是否预览旋转
				circular:false
			}
		},
		onLoad() {
			wx.showShareMenu({
			  withShareTicket: true
			})
		},
		methods: {
			//图片预览
			imgPreview(imgList,index){
				if(imgList == 'icon'){
					this.imgList = [this.info.iconSrc]
					index = 0;
					this.circular = false;
				}else{
					this.imgList = imgList;
					this.circular = true;
				}
				this.$refs.previewImage.open(index);
				// imgList.forEach((item,index)=>{
				// 	imgList[index] = this.baseUrl+item;
				// })
				// uni.previewImage({
				// 	current:index,
				// 	urls:imgList,
				// 	indicator:'number'
				// })
			}
		}
	}
</script>

<style >
	.top{
		background: #06a8ff;
		color: #FFFFFF;
		width: 100%;
		height: 300rpx;
		display: flex;
		padding: 20rpx;
		align-items: flex-end;
	}
	.top_inner{
		display: flex;
		margin: 15rpx;

	}
	.top_img{
		width: 200rpx;
		height: 200rpx;
		background: #fff;
		border-radius: 20rpx;
	}
	.top_right{
		display: flex;
		width: 65%;
		flex-direction: column;
		margin-left: 20rpx;
	}
	.text1{
		display: flex;
		margin-bottom: 20rpx;
	}
	.text2{
		display: flex;
	}
	.text3{
		padding-right: 20rpx;
	}
	.name{
		font-size: 42rpx;
		padding-right: 20rpx;
		font-weight: 600;
	}
	.flex{
		display: flex;
	}
	.info_block{
		margin: 20rpx 0 20rpx 0;
		background: #FFFFFF;
		padding: 20rpx;
		flex-direction: column;
	}
	.info_title{
		color: #06a8ff;
		font-weight: 600;
		margin: 20rpx;
	}
	.info_content{
		display: flex;
		margin-bottom: 20rpx;
	}
	.info_content_left{
		width: 28%;
	}
	.info_content_right{
		width: 70%;
	}
	.img_info{
		display: flex;
		background: #FFFFFF;
		flex-wrap: wrap;
		padding: 20rpx 10rpx 20rpx 30rpx;
	}
	.photo{
		width: 220rpx;
		height: 220rpx;
		margin-bottom: 20rpx;
		margin-right: 20rpx;
		border-radius: 20rpx;
		background: #f5f6f9;
	}
	.work{
		font-size: 32rpx;
		margin: 20rpx 0;
	}
	.work_timeq{
		color: #06a8ff;
		font-weight: 600;
		display: flex;
	}
	.dot{
		width: 20rpx;
		height: 20rpx;
		background: #06a8ff;
		border-radius: 30rpx;
		margin: 16rpx 10rpx;
	}
	.work_info{
		margin-left: 40rpx;
	}
</style>
