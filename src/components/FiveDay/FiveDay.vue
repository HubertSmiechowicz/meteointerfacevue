<script setup lang="ts">
import { ref, onMounted, computed } from 'vue';
import { LineChart } from 'vue-chart-3';
import { Chart, registerables } from 'chart.js';
import axios, { AxiosResponse } from 'axios';
import MainData from '../Template/MainData.vue';

Chart.register(...registerables);

const baseUrl = 'https://meteonowapi.azurewebsites.net/';
const cityName = ref<string>('');
const temperature = ref<number>(0);
const description = ref<string>('');
const tempMax = ref<number>(0);
const image = ref<string>('');
const days = ref<string[]>([]);
const temperatureList = ref<number[]>([]);
const imageList = ref<string[]>([]);

const setWeather = (response: AxiosResponse) => {
  cityName.value = response.data.name;
  temperature.value = response.data.temp;
  description.value = response.data.description;
  image.value = response.data.image;
};

interface ForecastDto {
  dt: string;
  temp: number;
  image: string;
}

const setChartData = (
  response: AxiosResponse<{ forecastDtos: ForecastDto[] }>
) => {
  response.data.forecastDtos.forEach((forecast) => {
    days.value.push(forecast.dt);
    temperatureList.value.push(forecast.temp);
    imageList.value.push(forecast.image);
  });
};

onMounted(() => {
  axios
    .get(`${baseUrl}presentdayforecast?cityName=Warszawa`)
    .then((response) => {
      setWeather(response);
    })
    .then(() => {
      axios
        .get(`${baseUrl}fivedaysforecast?cityName=Warszawa`)
        .then((response) => {
          setChartData(response);
        });
    });
});

const getWeather = (city: string) => {
  axios
    .get(`${baseUrl}presentdayforecast?cityName=${city}`)
    .then((response) => {
      setWeather(response);
    })
    .then(() => {
      days.value = [];
      temperatureList.value = [];
      axios
        .get(`${baseUrl}fivedaysforecast?cityName=${city}`)
        .then((response) => {
          setChartData(response);
        });
    });
};

const data = computed(() => ({
  labels: days.value,
  datasets: [
    {
      data: temperatureList.value,
      borderColor: '#60a5fa',
    },
  ],
}));

const options = {
  responsive: true,
  plugins: {
    title: {
      display: true,
      font: {
        size: 24,
      },
      text: 'Prognoza pogody na pięć dni ',
      color: '#60a5fa',
    },
    legend: {
      display: false,
    },
  },
  scales: {
    x: {
      grid: {
        display: false,
      },
      ticks: {
        font: {
          size: 15,
        },
        color: '#60a5fa',
      },
    },
    y: {
      max: 30,
      min: -20,
      grid: {
        display: false,
      },
      ticks: {
        stepSize: 10,
        font: {
          size: 15,
        },
        color: '#60a5fa',
      },
    },
  },
};
</script>

<template>
  <div class="h-full w-full text-blue-400 dark:text-slate-50">
    <MainData
      :height="'h-3/6 sm:h-2/6 '"
      :baseUrl="baseUrl"
      :name="cityName"
      :temperature="temperature"
      :description="description"
      :tempMax="tempMax"
      :image="image"
      @get-weather="getWeather"
    />

    <LineChart
      :chartData="data"
      :options="options"
      class="h-3/6 sm:h-4/6 w-full pb-3 border-b-4 rounded-xl border-slate-50 dark:border-slate-800 bg-blue-100 dark:bg-slate-700"
    />
  </div>
</template>

<style scoped></style>
