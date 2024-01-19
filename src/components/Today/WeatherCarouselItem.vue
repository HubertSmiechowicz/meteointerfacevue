<script setup lang="ts">
import { getCurrentInstance } from 'vue';

const props = defineProps<{ name: string; temp: number; image: string }>();

const instance = getCurrentInstance();

const getWeather = () => {
	if (instance) {
		instance.emit('get-weather', props.name);
	}
};
</script>

<template>
	<div
		class="w-full flex flex-col items-center justify-center hover:cursor-pointer"
		@click="getWeather">
		<img :src="props.image" alt="weather picture" class="w-16 h-16" />
		<div class="w-full flex justify-center">
			<p class="mr-3">{{ props.name }}</p>
			<p>{{ props.temp }}°</p>
		</div>
	</div>
</template>

<style scoped></style>
