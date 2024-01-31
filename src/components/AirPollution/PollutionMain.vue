<script setup lang="ts">
	const props = defineProps<{
		descriptionPollution: string;
		imagePollution: string;
		pm2_5: number;
	}>();
</script>

<template>
	<div class="h-full w-1/3 flex items-center justify-center text-sm sm:text-xl">
		<div
			class="h-3/4 w-3/4 flex flex-col justify-between items-center bg-slate-50 dark:bg-slate-800 border-t-8 border-r-8 border-l-8 rounded-3xl border-blue-100 dark:border-slate-700">
			<div
				class="h-1/6 w-full flex justify-center items-center border-b border-blue-200">
				<p>{{ props.descriptionPollution }}</p>
			</div>
			<img
				:src="props.imagePollution"
				alt="Air pollution picture"
				class="h-4/6" />
			<div
				class="h-1/6 w-full flex justify-center items-center border-t border-blue-200">
				<p>PM {{ pm2_5 }}</p>
			</div>
		</div>
	</div>
</template>

<style scoped></style>
