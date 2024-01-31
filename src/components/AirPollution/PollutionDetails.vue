<script setup lang="ts">
	const props = defineProps<{
		co: number;
		no: number;
		no2: number;
		o3: number;
		so2: number;
		nh3: number;
	}>();
</script>

<template>
	<div class="h-full w-2/3 flex text-sm sm:text-lg items-center justify-around">
		<div
			class="h-5/6 w-full flex flex-col items-center justify-center bg-slate-50 dark:bg-slate-800 border-t-8 border-r-8 rounded-3xl border-blue-100 dark:border-slate-700">
			<div class="flex flex-col justify-center items-center">
				<p>Tlenek węgla</p>
				<p class="font-bold">{{ props.co }}</p>
			</div>
			<div class="m-5 flex flex-col justify-center items-center">
				<p>Tlenek azotu</p>
				<p class="font-bold">{{ props.no }}</p>
			</div>
			<div class="flex flex-col justify-center items-center">
				<p>Dwutlenek azotu</p>
				<p class="font-bold">{{ props.no2 }}</p>
			</div>
		</div>
		<div
			class="h-5/6 w-full flex flex-col items-center justify-center bg-slate-50 dark:bg-slate-800 border-t-8 border-r-8 rounded-3xl border-blue-100 dark:border-slate-700">
			<div class="flex flex-col justify-center items-center">
				<p>Ozon</p>
				<p class="font-bold">{{ props.o3 }}</p>
			</div>
			<div class="m-5 flex flex-col justify-center items-center">
				<p>Dwutlenek siarki</p>
				<p class="font-bold">{{ props.so2 }}</p>
			</div>
			<div class="flex flex-col justify-center items-center">
				<p>Amoniak</p>
				<p class="font-bold">{{ props.nh3 }}</p>
			</div>
		</div>
	</div>
</template>

<style scoped></style>
