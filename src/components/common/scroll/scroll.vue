<template>
	<div class="wrapper" ref="wrapper">
		<div class="content">
			<slot></slot>
		</div>
	</div>
</template>

<script>
	import BScroll from 'better-scroll'
	export default {
		name: "scroll.vue",
		props: {
			probeType: {
				type: Number,
				default: 0
			},
			pullUpLoad: {
				type: Boolean,
				default: false
			}
		},
		data() {
			return {
				scroll: null
			}
		},
		mounted() {
			// 1.创建BScroll对象
			this.scroll = new BScroll(this.$refs.wrapper, {
				click: true,
				probeType: this.probeType,
				pullUpLoad: this.pullUpLoad
			})

			// 2.监听滚动位置
			if(this.probeType === 2 || this.probeType ===3) {
				this.scroll.on('scroll', (position) => {
					this.$emit('scroll', position)
				})
			}

			// 3.监听上拉加载更多
			if(this.pullUpLoad) {
				this.scroll.on('pullingUp', () => {
					this.$emit('pullingUp')
				})
			}
		},
		methods: {
			scrollTo(x, y, time=300) {
				this.scroll.scrollTo(x, y, time)
			},
			finishPullUp() {
				this.scroll.finishPullUp()
			},
			refresh() {
				// 由于图片的异步加载，故需要重新计算可滚动的高度
				this.scroll.refresh()
			},
			getScrollY() {
				return this.scroll ? this.scroll.y : 0
			}
		}
	}
</script>

<style scoped>
	
</style>