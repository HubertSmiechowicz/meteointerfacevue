<script setup lang="ts">
	import PollutionMain from './PollutionMain.vue';
	import PollutionDetails from './PollutionDetails.vue';

	const props = defineProps<{
		descriptionPollution: string;
		imagePollution: string;
		co: number;
		no: number;
		no2: number;
		o3: number;
		so2: number;
		pm2_5: number;
		nh3: number;
	}>();
</script>

<template>
	<div
		class="h-3/6 sm:h-4/6 w-full flex justify-center items-center pb-3 border-b-4 rounded-xl border-slate-50 dark:border-slate-800 bg-blue-100 dark:bg-slate-700">
		<PollutionMain
			:descriptionPollution="descriptionPollution"
			:imagePollution="imagePollution"
			:pm2_5="pm2_5" />
		<PollutionDetails
			:co="co"
			:no="no"
			:no2="no2"
			:o3="o3"
			:so2="so2"
			:nh3="nh3" />
	</div>
</template>

<style scoped></style>
