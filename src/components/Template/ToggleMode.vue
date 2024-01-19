<script setup lang="ts">
import { getCurrentInstance } from 'vue';
import { SunMoon } from 'lucide-vue-next';

const instance = getCurrentInstance();

const toggleMode = () => {
	if (instance) {
		instance.emit('toggle-mode');
	}
};
</script>

<template>
	<SunMoon
		class="mx-3 w-8 h-8 hover:cursor-pointer hover:text-blue-300 dark:hover:text-blue-300 text-blue-500 dark:text-slate-50"
		@click="toggleMode"
		>Click</SunMoon
	>
</template>

<style scoped></style>
