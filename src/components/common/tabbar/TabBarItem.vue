<template>
	<div class="tab-bar-item" @click='itemClick'>
		<div v-if="!isActive"><slot name='item-icon'></slot></div>
		<div v-else><slot name='item-icon-active'></slot></div>
		<div :style='activeStyle'><slot name='item-text'></slot></div>
	</div>
</template>

<script>
	export default {
		name: "TabBarItem",
		props: {
			path: String,
			activeColor: {
				type: String,
				default: 'red'
			}
		},
		data() {
			return {
				// isActive: false
			}
		},
		computed: {
			isActive: {
				get() {
					return this.$route.path.indexOf(this.path) !== -1
				},
				set() {
					return this.$route.path.indexOf(this.path) !== -1
				}
			},
			activeStyle() {
				return this.isActive ? {color: this.activeColor} : {}
			}
		},
		methods: {
			itemClick() {
				this.$router.replace(this.path)
				this.isActive = !this.isActive
			}
		}
	}
</script>

<style scoped>
.tab-bar-item {
  flex: 1;
  text-align: center;
  height: 49px;
  font-size: 14px;
}

.tab-bar-item img{
	width: 24px;
	height: 24px;
	margin-top: 3px;
	/*去除图片默认留空3px*/
	vertical-align: middle;
}

.active {
	color: red;
}
</style>