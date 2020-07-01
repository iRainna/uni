<template>
	<view>
		<view v-if="!isDuanWang">
			
		</view>
		<!-- 断网 -->
		<duan-wang :duanWang="isDuanWang"></duan-wang>
	</view>
</template>

<script>
	import duanWang from '@/components/duanWang/duanWang.vue';
	export default {
		components:{
			duanWang
		},
		data() {
			return {
				// 断网：
				isDuanWang: false
			}
		},
		methods: {
			
		}
	}
</script>

<style>
page{
	background: #F7F7F7;
}

</style>
