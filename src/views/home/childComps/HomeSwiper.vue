<template>
	<div>
		<swiper>
			<swiper-item	v-for="(item, itemIndex) in banners" 
										:key="itemIndex">
				<a :href="item.link">
					<img :src="item.image" alt="" @load='imageLoad'>
				</a>
			</swiper-item>
		</swiper>
	</div>
</template>

<script>
	import {Swiper, SwiperItem} from 'components/common/swiper/index'

	export default {
		name: "HomeSwiper",
		data() {
			return {
				isLoad: false
			}
		},
		components: {
			Swiper,
			SwiperItem
		},
		props: {
			banners: {
				type: Array,
				default() {
					return []
				}
			}
		},
		methods: {
			imageLoad() {
				if(!this.isLoad) {
					this.$emit('swiperImageLoad')
					this.isLoad = true
				}
			}
		}
	}
</script>

<style scoped>
	
</style>