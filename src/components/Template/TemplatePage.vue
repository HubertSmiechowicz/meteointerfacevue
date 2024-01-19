<script setup lang="ts">
import { ref, computed } from 'vue';
import Brand from './Brand.vue';
import ToggleMode from './ToggleMode.vue';
import Navigation from './Navigation.vue';
import Home from '../Home/Home.vue';
import Today from '../Today/Today.vue';

const routes = {
	'/': Home,
	'/today': Today,
};

const currentPath = ref(window.location.hash);

window.addEventListener('hashchange', () => {
	currentPath.value = window.location.hash;
});

const currentView = computed(() => {
	return routes[currentPath.value.slice(1) || '/'];
});

const darkMode = ref<string>('');

const toggleModeFunction = () => {
	darkMode.value = darkMode.value === 'dark' ? '' : 'dark';
};
</script>

<template>
	<div :class="darkMode" class="font-montserrat">
		<div
			id="screen"
			class="h-screen w-full flex flex-col justify-between bg-slate-50 dark:bg-slate-800">
			<nav
				id="nav"
				class="w-full h-20 flex justify-between items-center md:border-b border-blue-500 dark:border-slate-50">
				<div class="flex items-center">
					<Brand />
					<Navigation />
				</div>
				<ToggleMode @toggle-mode="toggleModeFunction" />
			</nav>
			<main class="container h-full w-full">
				<component :is="currentView" />
			</main>
			<footer
				class="h-8 w-full flex justify-center items-center text-sm border-t text-blue-300 border-blue-500 dark:text-slate-300 dark:border-slate-50">
				Lodz 2024
			</footer>
		</div>
	</div>
</template>

<style scoped></style>
