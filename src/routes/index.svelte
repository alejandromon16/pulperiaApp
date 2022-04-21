<script>
	import Counter from '$lib/Counter.svelte';
	import Logo from '$lib/Logo.svelte';
	import { browser } from '$app/env';
	import { goto } from '$app/navigation' ;
	import { fade, slide } from 'svelte/transition';

	let desktop;

	if (browser) {
		window.api.receive('from-main', (data) => {
			desktop = `Received Message "${data}" from Electron`;
			console.log(desktop);
		});
	}

	let password;
	let error = '';

	const checker = () => {
		if(password == '123'){
			goto('/admin/')
		}else{
			error = "contrasena no es valida"
		}
	}

</script>

<main>
	
	<div out:fade={{duration:300}}>
		<div class="grid grid-cols-2 bg-white">
			<div class="grid place-content-center w-full max-w-xs">
				<form class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
				  <div class="mb-6">
					<h1  in:slide={{duration:200}} class="text-red-300 text-left">{error}</h1>
					<label class="text-left block text-gray-700 text-sm font-bold mb-2" for="password">
					  Ingrese la Contrasena
					</label>
					<input bind:value={password} class="appearance-none border-b-2 border-black w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline" id="password" type="password">
					
				</div>
				  <div class="flex items-center justify-end">
					<button on:click={() => checker()} class="bg-[#1e2881] hover:bg-[#0e1346] text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" type="button">
					  Ingresar
					</button>
				  </div>
				</form>
				<p class="text-center text-gray-500 text-xs">
				  &copy;2020 SoftCruz Corp. All rights reserved.
				</p>
			  </div>
			<div class="relative">
				<div class="absolute top-[40%] text-white font-base text-4xl">Bienvenido a <b class="font-bold">SoftCruz SRL</b></div>
				<div>
					<img class="h-screen w-full" src="https://img.freepik.com/free-vector/abstract-dark-blue-background-with-overlapping-stripe_500223-232.jpg?size=626&ext=jpg" alt="">
				</div>
			</div>
		</div>
	</div>

	{#if desktop}
		<br />
		<br />
		{desktop}
	{/if}
</main>

<style>
	:root {
		font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu,
			Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
	}

	:global(body) {
		margin: 0;
		padding: 0;
	}

	main {
		padding: 2em 1em 1em 1em;
		text-align: center;
		animation: fade 1s;
		margin: 0 auto;
	}

	@keyframes fade {
		from {
			opacity: 0;
		}
		to {
			opacity: 1;
		}
	}
</style>
