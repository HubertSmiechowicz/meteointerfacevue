<script setup lang="ts"></script>

<template>
	<div
		class="h-full w-full flex flex-col justify-center items-center text-blue-400 dark:text-slate-50">
		<img
			class="rounded-full"
			src="https://www.dropbox.com/scl/fi/96v22sly4yxxibrtyxqyf/meteobrand.png?rlkey=bu88fb6821zfqqkgcfmwretza&dl=1"
			alt="meteo brand" />
		<p class="font-bold my-5">Witaj w MeteoNow</p>
		<div class="flex flex-col justify-center items-center">
			<p>
				Dzięki nam możesz sprawdzić prognozę pogody dla wielu miejsc na świecie.
				Interesuje cię temperatura, ciśnienie atmosferyczne, wilgotność a może
				to jak silny będzie wiatr?
			</p>
			<p>
				U nas znajdziesz to wszystko, ale nie tylko. Mamy przygotowaną również
				prognozę na pięć dni oraz aktualną jakość powietrza. Nie zwlekaj i
				sprawdź pogodę na:
			</p>
		</div>
		<a
			href="#/today"
			class="text-blue-500 text-3xl font-bold mt-5 dark:text-slate-50 hover:cursor-pointer hover:text-blue-300 dark:hover:text-blue-300">
			Dziś
		</a>
	</div>
</template>

<style scoped></style>
