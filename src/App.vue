<script setup lang="ts">
import { defineComponent } from 'vue';
import Footer from "./components/Footer.vue"

</script>

<template>
	<div class="app">
		<div class="content">
			<aside class="app__sidebar">
				<div class="sidebar__image"></div>
				<div class="sidebar__content">
					<h2 class="sidebar__title">Title</h2>
					<p class="sidebar__description">Description goes here.</p>
				</div>
			</aside>
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
	padding: 2rem;
}

.content {
	display: flex;
	justify-content: space-between;
}

.app__sidebar {
	background-color: #4d4d4d;
	min-width: 31.2rem;
}
</style>
