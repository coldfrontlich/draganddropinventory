<template>
	<div class="modal-overlay" @click.self="$emit('close')">
		<div class="modal-content">
			<button class="close-button" @click="$emit('close')">&times;</button>
			<div class="modal-body">
				<img
					v-if="itemSrc"
					:src="itemSrc"
					alt="Selected item"
					class="modal-image"
				/>
				<Skeleton v-for="index in 5" :key="index" :height="10" />
				<button class="delete-button" @click="$emit('delete')">
					Удалить предмет
				</button>
			</div>
		</div>
	</div>
</template>

<script setup lang="ts">
import Skeleton from './Skeleton.vue';
defineProps<{ itemSrc: string | null }>()
defineEmits(['close', 'delete'])
</script>

<style scoped>
.modal-overlay {
	position: absolute;
	top: 0;
	right: 0;
	bottom: 0;
	left: 0;
	background-color: rgba(0, 0, 0, 0.5);
	display: flex;
	justify-content: flex-end;
	z-index: 1000;
	animation: fadeIn 0.3s ease-out;
}

.modal-content {
	position: relative;
	top: 4%;
	right: 20%;
	background-color: #262626;
	width: 300px;
	height: 74vh;
	padding: 20px;
	box-shadow: -2px 0 8px rgba(0, 0, 0, 0.25);
	border-radius: 8px;
	animation: scaleIn 0.3s ease-out;
}

.modal-body {
	display: flex;
	flex-direction: column;
	height: 100%;
	align-items: center;
	justify-content: center;
	gap: 2rem;
}

.modal-image {
	max-width: 200px;
	max-height: 200px;
	object-fit: contain;
}

.delete-button {
	padding: 12px 24px;
	background-color: #ff4444;
	color: white;
	border: none;
	border-radius: 6px;
	cursor: pointer;
	font-size: 1rem;
}

.close-button {
	position: absolute;
	top: 10px;
	right: 10px;
	background: none;
	border: none;
	font-size: 24px;
	color: white;
	cursor: pointer;
}

.close-button:hover {
	color: #ff4444;
}

/* Анимации */
@keyframes fadeIn {
	from {
		opacity: 0;
	}
	to {
		opacity: 1;
	}
}

@keyframes scaleIn {
	from {
		transform: scale(0.9);
		opacity: 0;
	}
	to {
		transform: scale(1);
		opacity: 1;
	}
}
</style>
