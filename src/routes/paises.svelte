<script context="module">
	export async function preload() {
		const res = await this.fetch('https://corona.lmao.ninja/v2/countries?yesterday&sort');
		const countries = await res.json();

		return { countries };
	}
</script>

<script>
	export let countries;

  let nf = new Intl.NumberFormat('de-DE');

	countries.sort((a, b) => {
		if (a.cases < b.cases) {
			return 1;
		} else if (a.cases > b.cases) {
			return -1;
		} else {
			return 0;
		}
	});

	function showMore(idPlus, idData) {
		let more = document.getElementById(`${idPlus}`);
		let data = document.getElementById(`${idData}`);
		console.log(more)
		console.log(data)
		const watcher = data.classList.contains('hidden');
		console.log(watcher)

		if (watcher === true) {
			more.classList.add('rotate-45');
			data.classList.remove('hidden');
		} else {
			more.classList.remove('rotate-45');
			data.classList.add('hidden');
		}
	}
</script>

<style>
	figcaption {
		width: fit-content;
	}

	.country {
		height: fit-content;
	}
</style>

<svelte:head>
	<title>Países</title>
</svelte:head>

<section class="container mx-auto pt-1 md:grid md:grid-cols-2 md:col-gap-6 lg:-mt-4 xl:grid-cols-3">
	{#each countries as {countryInfo, country, todayCases, todayRecovered, todayDeaths, cases, deaths, recovered, tests, active, critical}}
		<div class="country grid grid-cols-2 bg-gray-100 rounded-lg shadow mb-6 max-w-md mx-auto lg:mb-8">
			<figure class="relative text-center h-32">
				<img class="h-32 w-full object-center rounded-tl-lg" src={countryInfo.flag} alt="item.country">
				<figcaption on:click={showMore(countryInfo.iso2, countryInfo.iso3)} class="absolute bg-gray-100 truncate cursor-pointer bottom-0 font-bold pl-1 pr-4 shadow-inner rounded-tr-full">
					{country} <i id={countryInfo.iso2} class="text-sm transition-transform duration-700 transform fas fa-plus-circle"></i>
				</figcaption>
			</figure>
			<div class="text-center py-2 h-32">
				<h3 class="font-bold">Hoy:</h3>
				{#if todayCases == 0 && todayRecovered == 0 && todayDeaths == 0}	
					<p class="mt-2 truncate">Aún no hay reportes</p>
				{:else}
					<p class="mt-2 truncate">{nf.format(todayCases)} {#if todayCases == 1}caso{:else} casos{/if}</p>
					<p class="truncate">{nf.format(todayRecovered)} {#if todayRecovered == 1}recuperado{:else}recuperados{/if}</p>
					<p class="truncate">{nf.format(todayDeaths)} {#if todayDeaths == 1}muerto{:else}muertos{/if}</p>
				{/if}
			</div>
			<div id={countryInfo.iso3} class="hidden col-span-2 grid grid-cols-2 italic bg-gray-100 shadow-inner text-center py-4">
				<div class="px-4">
					<p class="truncate">{nf.format(cases)} {#if todayCases == 1}caso{:else} casos{/if}</p>
					<p class="truncate">{nf.format(recovered)} {#if todayRecovered == 1}recuperado{:else}recuperados{/if}</p>
					<p>{nf.format(deaths)} {#if todayDeaths == 1}muerto{:else}muertos{/if}</p>
				</div>
				<div class="px-4">
					<p class="truncate">{nf.format(tests)} {#if tests == 1}prueba{:else}pruebas{/if}</p>
					<p class="truncate">{nf.format(active)} {#if active == 1}activo{:else}activos{/if}</p>
					<p class="truncate">{nf.format(critical)} en estado crítico</p>
				</div>
			</div>
		</div>
	{/each}
</section>