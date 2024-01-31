<script setup lang="ts">
	import { getCurrentInstance } from 'vue';
	import CitySearch from './CitySearch.vue';

	const props = defineProps<{
		height: string;
		baseUrl: string;
		name: string;
		temperature: number;
		description: string;
		tempMax: number;
		image: string;
	}>();

	const today = new Date();

	const formatMonth = () => {
		if (today.getMonth() + 1 < 10) {
			return `0${today.getMonth() + 1}`;
		} else {
			return today.getMonth() + 1;
		}
	};

	const instance = getCurrentInstance();

	const getWeather = (city: string) => {
		if (instance) {
			instance.emit('get-weather', city);
		}
	};
</script>

<template>
	<div :class="props.height">
		<CitySearch :base-url="props.baseUrl" @get-weather="getWeather" />
		<div class="h-4/5 flex justify-between">
			<div class="flex flex-col justify-around">
				<div>
					<p class="text-3xl font-bold">{{ props.name }}</p>
					<p class="text-sm dark:text-slate-400">
						{{ `${today.getDate()}.${formatMonth()}.${today.getFullYear()}` }}
					</p>
				</div>
				<div>
					<p class="text-5xl font-bold">{{ props.temperature }}°</p>
					<p class="dark:text-slate-400 first-letter:uppercase">
						{{ props.description }}. Maksymalna temperatura dziś osiągnie
						{{ $props.tempMax }}°
					</p>
				</div>
			</div>
			<div class="flex justify-center items-center">
				<img :src="props.image" alt="Weather picture" />
			</div>
		</div>
	</div>
</template>

<style scoped></style>
