<script>
	export let countries;
	export let index;

	let language;
  let nf = new Intl.NumberFormat('de-DE');

	$: if (index === 'es') {
		language = new TranslateCountries('Hoy', 'Casos', 'Recuperados', 'Muertes', 'País', 'Aún no hay reportes', 'Ver más');
	} else if (index === 'en') {
		language = new TranslateCountries('Today', 'Cases', 'Recovereds', 'Deaths', 'Country', 'No reports yet', 'See more');
	}
	countries.sort((a, b) => {
		if (a.cases < b.cases) {
			return 1;
		} else if (a.cases > b.cases) {
			return -1;
		} else {
			return 0;
		}
	});

  class TranslateCountries {
    constructor(today, cases, recovered, deaths, country, report, more) {
      this.today = today;
      this.cases = cases;
      this.recovered = recovered;
			this.deaths = deaths;
			this.country = country;
			this.report = report;
			this.more = more;
    }
  }
</script>

<style>
	@media (max-width: 640px) {
		td, th {
			font-size: 0.75rem;
		}
	}

	@media (max-width: 480px) {
		td {
		font-size: 0.6rem;
		}

		th {
			font-size: 0.6rem;
		}
	}
</style>

<section class="container mx-auto">
 <table class="text-center mx-auto w-full sm:text-sm md:text-base">
    <thead>
			<tr>
				<th></th>
				<th></th>
				<th class="hidden lg:table-cell"></th>
				<th class="hidden lg:table-cell"></th>
				<th class="hidden lg:table-cell"></th>
				<th class="bg-teal-600 rounded-tl-md border-b border-teal-800 border-opacity-25"></th>
				<th class="bg-teal-600 py-1 border-b border-teal-800 border-opacity-25">{language.today}</th>
				<th class="bg-teal-600 rounded-tr-md border-b border-teal-800 border-opacity-25"></th>
				<th></th>
			</tr>
      <tr class="border-b-2 border-gray-400 bg-teal-700 shadow-inner">
				<th class="rounded-tl-md"></th>
				<th class="py-1 lg:pt-2">{language.country}</th>
				<th class="hidden lg:table-cell">{language.cases}</th>
				<th class="hidden lg:table-cell px-2">{language.recovered}</th>
				<th class="hidden lg:table-cell">{language.deaths}</th>
				<th class="bg-teal-600 px-3 md:px-5 xl:px-6">{language.cases}</th>
				<th class="bg-teal-600 px-2">{language.recovered}</th>
				<th class="bg-teal-600 px-2 md:px-3">{language.deaths}</th>
				<th class="rounded-tr-md"></th>
      </tr>
    </thead>
    <tbody class="bg-teal-700 shadow-inner">
			{#each countries as { countryInfo, country, cases, recovered, deaths, todayCases, todayRecovered, todayDeaths }}
				<tr class="border-b border-gray-300">
					<td class="w-16 sm:w-20 py-1 pl-1 sm:pl-2 md:w-24 md:py-2">
						<img
							class="h-8 w-16 mx-auto sm:h-12 sm:w-20 md:h-16 md:w-24 rounded-sm object-cover"
							src={countryInfo.flag}
							alt={country}
						>
					</td>
					<td class="pr-2">{country}</td>
					<td class="hidden lg:table-cell px-4">{nf.format(cases)}</td>
					<td class="hidden lg:table-cell">{nf.format(recovered)}</td>
					<td class="hidden lg:table-cell px-6">{nf.format(deaths)}</td>
					{#if todayCases == 0 && todayRecovered == 0 && todayDeaths == 0}
						<td class="bg-teal-600"></td>
						<td class="bg-teal-600">{language.report}</td>
						<td class="bg-teal-600"></td>
					{:else}
						<td class="bg-teal-600 px-2">{nf.format(todayCases)}</td>
						<td class="bg-teal-600 px-2">{nf.format(todayRecovered)}</td>
						<td class="bg-teal-600">{nf.format(todayDeaths)}</td>
					{/if} 
					<td class="w-16 sm:w-24 md:w-32 lg:w-24 xl:w-32 hover:underline cursor-pointer">{language.more}</td>
				</tr>
			{/each}
    </tbody>
  </table>
</section>