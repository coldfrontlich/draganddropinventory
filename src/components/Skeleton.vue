<template>
	<div class="skeleton-wrapper">
		<div class="skeleton" :style="{ height: height + 'px' }"></div>
	</div>
</template>

<style scoped>
.skeleton-wrapper {
	width: 100%;
	display: flex;
	justify-content: center;
}

.skeleton {
	width: 90%;
	background: linear-gradient(90deg, #3c3c3c 25%, #444444 50%, #333333 75%);
	background-size: 200% 100%;
	animation: loading 1.5s infinite linear;
	border-radius: 10px;
  margin-top: 10px;
  margin-bottom: 10px;
}

@keyframes loading {
	0% {
		background-position: 200% 0;
	}
	100% {
		background-position: -200% 0;
	}
}
</style>

<script setup lang="ts">
import { defineProps, withDefaults } from 'vue'

interface Props {
  height?: number
}

const props = withDefaults(defineProps<Props>(), {
  height: 40, 
});
</script>
