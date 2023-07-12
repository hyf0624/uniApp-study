<template>
	<view>
		<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000" :circular="true">
			<swiper-item v-for="(item, index) in swiperList" :key="index">
				<navigator :url="`/subpkg/goods_detail/goods_detail?goods_id=${item.goods_id}`" class="swiper-item">
					<image :src="item.image_src"></image>
				</navigator>
			</swiper-item>
		</swiper>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				// 轮播图的数据列表
				swiperList: []
			}
		},
		methods: {
			async getSwiperList() {
				const { data: res } = await uni.$http.get('/api/public/v1/home/swiperdata')
				if (res.meta.status === 200) {
					console.log(res)
					this.swiperList = res.message

				} else {
					uni.showToast({
						title: '数据请求失败',
						duration: 1500,
						icon: 'none'
					})
				}
			}
		},
		onLoad() {
			// 获取轮播图的数据
			this.getSwiperList()
		}
	}
</script>

<style lang="scss">
	swiper {
		height: 330rpx;

		.swiper-item,
		image {
			height: 100%;
			width: 100%;
		}
	}
</style>