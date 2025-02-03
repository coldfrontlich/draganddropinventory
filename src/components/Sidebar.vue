<template>
	<aside class="app__sidebar">
		<div class="sidebar__image">
			<img src="../assets/images/Blur.png" alt="sidebar image"/>
		</div>
		<div class="sidebar__content">
			<div class="skeleton_container main">
				<Skeleton :height="26" />
			</div>
			<Skeleton v-for="index in 5" :key="index" :height="10" />
			<div class="skeleton_container bottom">
				<Skeleton :height="10" />
			</div>
		</div>
	</aside>
</template>

<script setup lang="ts">
import Skeleton from './Skeleton.vue'
</script>

<style scoped>
.app__sidebar {
	background-color: #262626;
	min-width: 236px;
	border-radius: 10px;
	border: 1px solid #3c3c3c;
	margin-right: 1.5rem;
}

.sidebar__image {
	padding: 14px;
}

.sidebar__content {
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
}

.skeleton_container.main {
	width: 200px;
}

.skeleton_container.bottom {
	margin-top: 20px;
	width: 80px;
}
</style>
