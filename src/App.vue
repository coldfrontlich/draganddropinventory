<script setup lang="ts">
import { defineComponent } from 'vue'
import Footer from './components/Footer.vue'
import Sidebar from './components/Sidebar.vue'
</script>

<template>
	<div class="app">
		<div class="content">
      <Sidebar />
			<main class="app__main">
				<div class="main__grid">
					<div class="grid__item grid__item--1">4</div>
					<div class="grid__item grid__item--2">2</div>
					<div class="grid__item grid__item--3">5</div>
				</div>
			</main>
		</div>
		<Footer />
	</div>
</template>

<style scoped>
.app {
	display: flex;
	flex-direction: column;
	justify-content: space-between;
	height: 100vh;
}

.content {
	display: flex;
	justify-content: space-between;
	flex-grow: 1;
	overflow: auto;
  padding: 2rem 2rem 1.5rem 2rem;
}

</style>
