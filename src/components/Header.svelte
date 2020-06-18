<script>
	import { onMount } from 'svelte';

	export let segment;

	let language;

	$: if (segment === 'en') {
		language = new Translate('en', 'Countries', 'En', 'en/countries')
	} else {
		language = new Translate('.', 'Países', 'Es', 'paises');
	}

	class Translate {
		constructor(home, countries, index, linkCountries) {
			this.home = home;
			this.countries = countries;
			this.index = index;
			this.linkCountries = linkCountries;
		}
	}

	onMount(() => {
		document.addEventListener('click', e => {
			let languages = document.getElementById('languages');
			let hidden = languages.classList.contains('hidden');
			let clic = e.target;
			let btn = document.getElementById('button');

			if (hidden === false && clic != btn) {
				languages.classList.add('hidden');
			}
		}, false);
	});

	function showHide() {
		let languages = document.getElementById('languages');
		let hidden = languages.classList.contains('hidden');

		if (hidden === true) {
			languages.classList.remove('hidden');
		} else {
			languages.classList.add('hidden');
		}
	};
</script>

<header class="py-3 px-4 md:px-6 lg:px-8 shadow bg-gray-100">
	<div class="container mx-auto flex justify-between items-center">
		<div class="flex items-center justify-between">
			<a id="logo" class="flex items-center justify-center" href={language.home}>
				<img class="h-8" src="coronavirus.svg" alt="logo">
				<h1 class="ml-2 text-xl font-bold">COVID-19</h1>
			</a>
		</div>
		<nav class="relative">
			<ul class="flex">
				<li class="mr-8 sm:mr-12 md:mr-16">
					<a href={language.linkCountries}>{language.countries}</a>
				</li>
				<li>
					<p on:click={showHide} id="button" class="cursor-pointer">{language.index} <i class="fas fa-sort-down"></i></p>
					<ul id="languages" class="hidden absolute bg-gray-100 px-5 py-3 mt-4 rounded-b-lg shadow-md right-0 z-40">
						<li class="mb-2">
							<a class="hover:underline" href="/">Español</a>
						</li>
						<li>
							<a class="hover:underline" href="en">English</a>
						</li>
					</ul>
				</li>
			</ul>
		</nav>
	</div>
</header>
