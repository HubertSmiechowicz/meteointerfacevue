<script setup lang="ts">
	import { AtSign } from 'lucide-vue-next';
	import { Phone } from 'lucide-vue-next';
	import { Github } from 'lucide-vue-next';
</script>

<template>
	<div
		class="h-full w-full flex flex-col justify-center items-center text-blue-400 dark:text-slate-50">
		<div class="flex justify-center items-center">
			<img src="/src/assets/meteobrand.png" alt="meteo brand" class="h-24 w-24 rounded-full" />
			<p class="h-1/6 font-bold text-3xl">Kontakt</p>
		</div>
		<div class="h-3/6 w-full flex flex-col justify-around items-center">
			<div class="w-full flex flex-col justify-center items-center text-lg">
				<div class="flex">
					<AtSign />
					<p>E-mail</p>
				</div>
				<p>hubert.smiechowicz@gmail.com</p>
			</div>
			<div class="w-full flex flex-col justify-center items-center text-lg">
				<div class="flex">
					<Phone />
					<p>Telefon</p>
				</div>
				<p>664892981</p>
			</div>
			<div class="w-full flex justify-center items-center text-lg">
				<Github />
				<a href="https://github.com/HubertSmiechowicz?tab=repositories"
					>Github</a
				>
			</div>
		</div>
	</div>
</template>

<style scoped></style>
