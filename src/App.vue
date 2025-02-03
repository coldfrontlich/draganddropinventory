<script setup lang="ts">
import { defineComponent } from 'vue'
import Footer from './components/Footer.vue'
import Sidebar from './components/Sidebar.vue'
import Grid from './components/Grid.vue'
</script>

<template>
	<div class="app">
		<div class="wrapper">
			<div class="content">
				<Sidebar />
				<main class="app__main">
					<Grid />
				</main>
			</div>
			<Footer />
		</div>
	</div>
</template>

<style scoped>
.app {
	display: flex;
	flex-direction: column;
	justify-content: center;
	height: 100vh;
}

.content {
	display: flex;
	flex-grow: 1;
	overflow: auto;
	padding: 2rem 2rem 1.5rem 2rem;
}

.wrapper {
  margin: auto
}
</style>
