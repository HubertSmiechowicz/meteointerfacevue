<script setup lang="ts">
import { Thermometer } from 'lucide-vue-next';
import { Droplets } from 'lucide-vue-next';
import { Gauge } from 'lucide-vue-next';
import { Wind } from 'lucide-vue-next';

const props = defineProps<{
	feelsLike: number;
	humidity: number;
	pressure: number;
	windSpeed: number;
}>();
</script>

<template>
	<div
		class="h-2/6 p-5 flex items-center justify-around border-slate-50 dark:border-slate-800 border-y-8 rounded-3xl bg-blue-100 dark:bg-slate-700">
		<div class="h-full w-full flex flex-col justify-around items-center">
			<div class="w-full h-full flex flex-col items-center justify-center">
				<div class="flex items-center">
					<Thermometer class="mr-2" />
					<p>Temp. Odczuwalna</p>
				</div>
				<p class="text-2xl font-bold">{{ props.feelsLike }}°</p>
			</div>
			<div class="w-full h-full flex flex-col items-center justify-center">
				<div class="flex items-center">
					<Droplets class="mr-2" />
					<p>Wilgotność</p>
				</div>
				<p class="text-2xl font-bold">{{ props.humidity }} %</p>
			</div>
		</div>
		<div class="h-full w-full flex flex-col justify-around items-start">
			<div class="w-full h-full flex flex-col items-center justify-center">
				<div class="flex items-center">
					<Gauge class="mr-2" />
					<p>Ciśnienie</p>
				</div>
				<p class="text-2xl font-bold">{{ props.pressure }} hPa</p>
			</div>
			<div class="w-full h-full flex flex-col items-center justify-center">
				<div class="flex items-center">
					<Wind class="mr-2" />
					<p>Prędkość wiatru</p>
				</div>
				<p class="text-2xl font-bold">{{ props.windSpeed }} m/s</p>
			</div>
		</div>
	</div>
</template>

<style scoped></style>
