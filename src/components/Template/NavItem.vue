<script setup lang="ts">
const props = defineProps<{
	content: string;
	href: string;
}>();
</script>

<template>
	<a
		:href="props.href"
		class="w-full h-full py-2 font-bold flex justify-center items-center hover:text-blue-300 dark:hover:text-blue-300 hover:cursor-pointer hover:rounded-3xl text-blue-500 dark:text-slate-50 md:mx-5">
		{{ props.content }}
	</a>
</template>

<style scoped></style>
