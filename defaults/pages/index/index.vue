<template>
	<view style="height: auto; width: 100%; display: inline-block;">
		<view style="height: auto; width: 100%;">
			<swiper style="width: 100%;" :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
				<swiper-item v-for="(item,index) in top_stories" :key="index" :data-newsid="item.id">
					
					<view style="position: absolute;top: 70px;">
						&emsp;{{item.title}}
					</view>
					<image :src="item.image" mode=""></image> 
				</swiper-item>
			</swiper>
		</view>
	<view class="">今日内容</view>
	<view class="content">
		<view class="uni-list">
			<view class="uni-list-cell" hover-class="uni-list-cell-hover" v-for="(item,index) in list" :key="index"
		@click="openinfo"	:data-id="item.id">
				<view class="uni-media-list">
					<image class="uni-media-list-logo" :src="item.images"></image>
					<view class="uni-media-list-body">
						<view class="uni-media-list-text-top">{{item.title}}</view>
					</view>
				</view>
			</view>
		</view>
	</view>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				list:[],
				top_stories:[]
			};
		},
		onLoad:function(){
			uni.request({
				url: 'https://news-at.zhihu.com/api/4/news/latest',
				method: 'GET',
				data: {},
				success: res => {
					this.list=res.data.stories;
					this.top_stories=res.data.top_stories
					console.log(this.top_stories);
				},
				fail: () => {},
				complete: () => {}
			});
		},
		methods:{
			openinfo(e){
				var id=e.currentTarget.dataset.id;
				uni.navigateTo({
					url: "../info/info?id="+id
				});
			}
		}
	}
</script>

<style>
.uni-media-list-body{height: auto;}
.uni-media-list-text-top{line-height: 1.6em;}

</style>
