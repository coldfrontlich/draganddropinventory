<template>
	<div class="app">
		<div class="app__wrapper">
			<div class="app__content">
				<Sidebar />
				<main class="app__main">
					<Grid />
				</main>
			</div>
			<Footer />
		</div>
	</div>
</template>

<script setup lang="ts">
import Sidebar from './components/Sidebar.vue'
import Grid from './components/Grid.vue'
import Footer from './components/Footer.vue';
</script>

<style scoped>
.app {
	display: flex;
	flex-direction: column;
	justify-content: center;
	height: 100vh;
}

.app__content {
	display: flex;
	flex-grow: 1;
	overflow: auto;
	padding: 2rem 2rem 1.5rem 2rem;
}

.app__wrapper {
  margin: auto
}
</style>
