<template>
	<footer class="footer">
		<div class="footer-content">
			<div class="skeleton-container">
				<Skeleton />
			</div>
			<span class="close-icon" @click="handleClose">&#10005;</span>
		</div>
	</footer>
</template>

<script setup>
import Skeleton from './Skeleton.vue'
</script>

<style lang="scss" scoped>
.footer {
	min-height: 60px;
	background-color: #262626;
	color: white;
	text-align: center;
	border-radius: 15px;
	display: flex;
	align-items: center;
	justify-content: center;
  margin-left: 2rem;
  margin-right: 2rem;
  margin-bottom: 2rem;
}

.footer-content {
	position: relative;
	width: 100%;
}

.close-icon {
	position: absolute;
	top: 2px;
	right: 10px;
	cursor: pointer;
	font-size: 14px;
}

.skeleton-container {
  padding-right: 3%;
}
</style>
