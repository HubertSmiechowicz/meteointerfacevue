<script setup lang="ts">
	import { ref, onMounted } from 'vue';
	import axios, { AxiosResponse } from 'axios';
	import MainData from '../Template/MainData.vue';
	import PollutionData from './PollutionData.vue';

	const baseUrl = 'http://localhost:5036/';
	const cityName = ref<string>('');
	const temperature = ref<number>(0);
	const description = ref<string>('');
	const tempMax = ref<number>(0);
	const image = ref<string>('');
	const descriptionPollution = ref<string>('');
	const imagePollution = ref<string>('');
	const co = ref<number>(0);
	const no = ref<number>(0);
	const no2 = ref<number>(0);
	const o3 = ref<number>(0);
	const so2 = ref<number>(0);
	const pm2_5 = ref<number>(0);
	const nh3 = ref<number>(0);

	const setWeather = (response: AxiosResponse) => {
		cityName.value = response.data.name;
		temperature.value = response.data.temp;
		description.value = response.data.description;
		image.value = response.data.image;
	};

	const setAirPollution = (response: AxiosResponse) => {
		descriptionPollution.value = response.data.descriptionPollution;
		imagePollution.value = response.data.imagePollution;
		co.value = response.data.co;
		no.value = response.data.no;
		no2.value = response.data.no2;
		o3.value = response.data.o3;
		so2.value = response.data.so2;
		pm2_5.value = response.data.pm2_5;
		nh3.value = response.data.nh3;
	};

	const getWeather = (city: string) => {
		axios
			.get(`${baseUrl}presentdayforecast?cityName=${city}`)
			.then(response => {
				setWeather(response);
				setAirPollution(response);
			})
			.then(() => {
				axios.get(`${baseUrl}airpollution?cityName=${city}`).then(response => {
					setAirPollution(response);
				});
			});
	};

	onMounted(() => {
		axios
			.get(`${baseUrl}presentdayforecast?cityName=Warszawa`)
			.then(response => {
				setWeather(response);
				setAirPollution(response);
			})
			.then(() => {
				axios.get(`${baseUrl}airpollution?cityName=Warszawa`).then(response => {
					setAirPollution(response);
				});
			});
	});
</script>

<template>
	<div class="h-full text-blue-400 dark:text-slate-50">
		<MainData
			:height="'h-3/6 sm:h-2/6'"
			:base-url="baseUrl"
			:name="cityName"
			:temperature="temperature"
			:description="description"
			:tempMax="tempMax"
			:image="image"
			@get-weather="getWeather" />
		<PollutionData
			:descriptionPollution="descriptionPollution"
			:imagePollution="imagePollution"
			:co="co"
			:no="no"
			:no2="no2"
			:o3="o3"
			:so2="so2"
			:pm2_5="pm2_5"
			:nh3="nh3" />
	</div>
</template>

<style scoped></style>
