<template>
	<view class="content">
		<view class="title">{{title}}</view>
		<view class="art-content">
			<rich-text class="richText" :nodes="strings"></rich-text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title:'',
				strings:''
			}
		},
		onLoad:function(e){
			uni.request({
				url: 'http://news-at.zhihu.com/api/2/news/'+e.id,
				method: 'GET',
				data: {},
				success: res => {
					this.title = res.data.title;
					this.strings = res.data.body;
				},
				fail: () => {},
				complete: () => {}
			});
		}
	}
</script>

<style>
	.content{padding: 10upx 2%;width: 96%;flex-wrap: wrap;}
	.title{line-height:2em;font-weight: 700;font-size: 38upx;}
	.art-content{line-height: 2em;}
</style>
