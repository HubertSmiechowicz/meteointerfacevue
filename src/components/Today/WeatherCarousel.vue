<script setup lang="ts">
	import { getCurrentInstance } from 'vue';
	import {
		Carousel,
		CarouselContent,
		CarouselItem,
		CarouselNext,
		CarouselPrevious,
	} from '../ui/carousel';
	import { Card, CardContent } from '../ui/card';
	import WeatherCarouselItem from './WeatherCarouselItem.vue';
	import Autoplay from 'embla-carousel-autoplay';

	const instance = getCurrentInstance();

	const getWeather = (city: string) => {
		if (instance) {
			instance.emit('get-weather', city);
		}
	};

	const props = defineProps<{
		citiesData: { name: string; temp: number; image: string }[] | undefined;
	}>();

	const plugin = Autoplay({
		delay: 2000,
		stopOnMouseEnter: true,
		stopOnInteraction: false,
	});
</script>

<template>
	<div
		class="h-1/6 p-3 flex items-center justify-center rounded-xl bg-blue-100 dark:bg-slate-700">
		<div class="w-full flex items-center justify-center">
			<Carousel
				class="relative w-3/4 sm:w-full max-w-xs md:max-w-md lg:max-w-lg"
				:opts="{
					align: 'start',
				}"
				:plugins="[plugin]"
				@mouseenter="plugin.stop"
				@mouseleave="[plugin.reset(), plugin.play()]">
				<CarouselContent>
					<CarouselItem
						v-for="city in props.citiesData"
						class="md:basis-1/2 lg:basis-1/3">
						<div class="p-1">
							<Card class="border-none">
								<CardContent class="flex items-center justify-center p-6">
									<WeatherCarouselItem
										:name="city.name"
										:temp="city.temp"
										:image="city.image"
										@get-weather="getWeather" />
								</CardContent>
							</Card>
						</div>
					</CarouselItem>
				</CarouselContent>
				<CarouselPrevious />
				<CarouselNext />
			</Carousel>
		</div>
	</div>
</template>

<style scoped></style>
