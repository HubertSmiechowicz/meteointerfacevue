<script setup lang="ts">
import { onMounted, ref } from 'vue';
import MainData from './MainData.vue';
import WeatherCarousel from './WeatherCarousel.vue';
import WeatherDatails from './WeatherDetails.vue';
import axios, { AxiosResponse } from 'axios';

const baseUrl = 'https://localhost:7257/';
const cityName = ref<string>('');
const temperature = ref<number>(0);
const description = ref<string>('');
const tempMax = ref<number>(0);
const image = ref<string>('');
const feelsLike = ref<number>(0);
const humidity = ref<number>(0);
const pressure = ref<number>(0);
const windSpeed = ref<number>(0);
const cities = ref<string[]>();
const citiesParams = ref<string>('');
const citiesData = ref<{ name: string; temp: number; image: string }[]>();

const setWeather = (response: AxiosResponse) => {
	cityName.value = response.data.name;
	temperature.value = response.data.temp;
	description.value = response.data.description;
	image.value = response.data.image;
	feelsLike.value = response.data.feelsLike;
	humidity.value = response.data.humidity;
	pressure.value = response.data.pressure;
	windSpeed.value = response.data.windSpeed;
	tempMax.value = response.data.tempMax;
};

onMounted(() => {
	axios
		.get(`${baseUrl}presentdayforecast?cityName=Warszawa`)
		.then((response) => {
			setWeather(response);
		})
		.then(() => {
			axios
				.get(`${baseUrl}cities/main`)
				.then((response) => {
					cities.value = response.data;
				})
				.then(() => {
					cities.value?.forEach((element) => {
						citiesParams.value += `cityNames=${element}&`;
					});
				})
				.then(() => {
					axios
						.get(`${baseUrl}presentdayforecast/cities?${citiesParams.value}`)
						.then((response) => {
							citiesData.value = response.data;
						});
				});
		});
});

const getWeather = (city: string) => {
	axios
		.get(`${baseUrl}presentdayforecast?cityName=${city}`)
		.then((response) => {
			setWeather(response);
		});
};
</script>

<template>
	<div class="h-full w-full text-blue-400 dark:text-slate-50">
		<MainData
			:base-url="baseUrl"
			:name="cityName"
			:temperature="temperature"
			:description="description"
			:tempMax="tempMax"
			:image="image"
			@get-weather="getWeather" />
		<WeatherCarousel :citiesData="citiesData" @get-weather="getWeather" />
		<WeatherDatails
			:feelsLike="feelsLike"
			:humidity="humidity"
			:pressure="pressure"
			:windSpeed="windSpeed" />
	</div>
</template>

<style scoped></style>
