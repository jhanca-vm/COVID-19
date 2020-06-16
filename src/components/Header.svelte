<script>
	import { onMount } from 'svelte';

	export let segment;

	onMount(() => {
		document.addEventListener('click', e => {
			let hidden = document.querySelector('nav').classList.contains('hidden');
			let click = e.target;
			let btnSwitch = document.getElementById('downUp');

			if (hidden == false && click != btnSwitch) {
				document.querySelector('nav').classList.add('hidden')
			}
		}, false);
	});

	function showHideMenu() {
		let hidden = document.querySelector('nav').classList.contains('hidden');
		let menu = document.querySelector('nav');
		
		if (hidden == true) {
			menu.classList.remove('hidden');
		} else {
			menu.classList.add('hidden');
		}
	};
</script>

<style>
	[aria-current] {
		position: relative;
	}

	[aria-current]::after {
		position: absolute;
		content: '';
		width: 100%;
		height: 2px;
		background-color: #2c7a7b;
		display: block;
		bottom: -1.28rem;
		opacity: .25;
	}

	#logo::after {
		display: none;
	}

	@media screen and (min-width: 640px) {
		#downUp {
			display: none;
		}
	}

	@media screen and (max-width: 640px) {
		[aria-current]::after {
			display: none;
		}
	}
</style>

<header class="py-3 px-4 md:px-6 lg:px-8 shadow bg-gray-100">
	<div class="container mx-auto sm:flex sm:justify-between sm:items-center">
		<div class="flex items-center justify-between">
			<a id="logo" class="flex items-center justify-center" aria-current="{segment === undefined ? 'page' : undefined}" href=".">
				<img class="h-8" src="coronavirus.svg" alt="logo">
				<h1 class="ml-2 text-xl font-bold">COVID-19</h1>
			</a>
			<i id="downUp" on:click={showHideMenu} class="ml-2 text-lg fas fa-chevron-down"></i>
		</div>
		<nav class="mt-3 hidden sm:block sm:m-0 shadow-inner sm:shadow-none -mb-3 py-1">
			<ul class="flex justify-between">
				<li class="sm:mr-8 md:mr-12">
					<a aria-current="{segment === 'about' ? 'page' : undefined}" href="about">Países</a>
				</li>
				<li class="sm:mr-8 md:mr-12">
					<a rel=prefetch aria-current="{segment === 'blog' ? 'page' : undefined}" href="blog">Continentes</a>
				</li>
				<li>
					<p>Es <i class="fas fa-sort-down"></i></p>
				</li>
			</ul>
		</nav>
	</div>
</header>
