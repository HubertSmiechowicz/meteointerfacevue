<script setup lang="ts">
import { ref, watch } from 'vue';
import { Menu } from 'lucide-vue-next';
import NavItem from './NavItem.vue';

const isHidden = ref<boolean>(false);
const menu = ref(null);

const changeDisplay = () => {
	if (menu.value)
		if (
			window.getComputedStyle(menu.value).getPropertyValue('display') === 'none'
		) {
			isHidden.value = false;
		} else {
			isHidden.value = true;
		}
};

// sprawdza podczas załadowania aplikacji jaki display ma menu
watch(menu, changeDisplay, { immediate: true });

// nasłuchuję na zmianę display menu
window.addEventListener('resize', changeDisplay);

const toggleMenu = () => {
	isHidden.value = !isHidden.value;
};
</script>

<template>
	<Menu
		ref="menu"
		:class="{
			'transform translate-x-0': isHidden,
			'transform translate-x-44': !isHidden,
		}"
		class="w-12 h-12 mx-3 transition-transform duration-300 ease-in-out md:hidden text-blue-500 dark:text-slate-50 hover:text-blue-300 dark:hover:text-blue-300 hover:cursor-pointer"
		@click="toggleMenu" />
	<div
		:class="{ 'translate-x-0': isHidden, 'translate-x-full': !isHidden }"
		class="h-screen w-64 fixed top-0 -left-64 transition-transform duration-300 ease-in-out border-r rounded-r-3xl border-blue-500 dark:border-slate-50 md:flex md:flex-row md:h-full md:w-full md:static md:left-0 md:translate-x-0 md:border-none bg-slate-50 dark:bg-slate-800">
		<div
			class="h-96 w-full flex flex-col justify-between items-center md:flex-row md:h-auto">
			<NavItem
				content="MeteoNow"
				href="#/"
				class="font-bold md:hidden"
				@click="toggleMenu" />
			<NavItem content="Dziś" href="#/today" @click="toggleMenu" />
			<NavItem content="Pięciodniowa" href="#/" @click="toggleMenu" />
			<NavItem content="Powietrza" href="#/" @click="toggleMenu" />
			<NavItem content="Mapy" href="#/" @click="toggleMenu" />
		</div>
	</div>
</template>

<style scoped></style>
