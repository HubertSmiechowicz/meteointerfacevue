<script setup lang="ts">
import { ref } from 'vue';
import axios from 'axios';
import { getCurrentInstance } from 'vue';

const props = defineProps<{ baseUrl: string }>();

const inputValue = ref<string>('');
const citiesValues = ref<string[]>();
const isListHidden = ref<boolean>(true);

const instance = getCurrentInstance();

const getWeather = (city: string) => {
	if (instance) {
		instance.emit('get-weather', city);
	}
	isListHidden.value = true;
	inputValue.value = '';
};

const getCities = () => {
	if (inputValue.value.length > 0) {
		axios
			.get(`${props.baseUrl}cities?cityNameFragment=${inputValue.value}`)
			.then((response) => {
				citiesValues.value = response.data;
			});
		isListHidden.value = false;
		console.log(isListHidden.value);
	} else if (inputValue.value.length === 0) {
		isListHidden.value = true;
		console.log(isListHidden.value);
	}
};
</script>

<template>
	<div class="h-1/5 flex justify-center items-center">
		<input
			type="text"
			placeholder="Wyszukaj miasto..."
			v-model="inputValue"
			@input="getCities"
			class="w-full p-1 rounded-xl text-slate-800 dark:text-slate-50 bg-blue-200 dark:bg-slate-700" />
	</div>
	<div
		:class="{ hidden: isListHidden, inline: !isListHidden }"
		class="fixed w-11/12 h-1/3 overflow-y-auto z-50 rounded-xl">
		<ul class="p-4 bg-blue-100 dark:bg-slate-700">
			<li
				v-for="city in citiesValues"
				@click="() => getWeather(city)"
				class="p-1 rounded-xl hover:cursor-pointer hover:bg-blue-200 dark:hover:bg-slate-600">
				{{ city }}
			</li>
		</ul>
	</div>
</template>

<style scoped></style>
