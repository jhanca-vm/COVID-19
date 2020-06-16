<script>
  export let countries;

  let numberFormat = new Intl.NumberFormat('de-DE');

  const API = 'https://corona.lmao.ninja/v2/all?yesterday';
  
  async function getData() {
    const response = await fetch(API);
    const data = await response.json();
    return data;
  };
</script>

<style>
  .text-7xl {
    font-size: 5rem;
    animation-name: rotate;
    animation-duration: 4s;
    animation-iteration-count: infinite;
    animation-timing-function: linear;
  }

  .column > p:last-child {
    padding-bottom: 0;
  }
</style>

<section class="container mx-auto text-center">
  {#await getData()}
    <i class="text-7xl text-red-400 mt-56 lg:mt-48 fas fa-virus"></i>
  {:then data}  
    <div class="text-gray-100 text-5xl">
      <div class="grid sm:grid-cols-2 lg:grid-cols-3 gap-6">
        <article class="bg-red-500 p-6 rounded-lg shadow-inner">
          <div class="border-b pb-5">
            <i class="fas fa-viruses"></i>
            <h2 class="font-bold">{numberFormat.format(data.cases)}</h2>
            <p class="text-2xl">Casos</p>
          </div>
          <p class="text-lg mt-5"><i>Hoy: +{numberFormat.format(data.todayCases)}</i></p>
        </article>
        <article class="bg-teal-500 p-6 rounded-lg shadow-inner">
          <div class="border-b pb-5">
            <i class="fas fa-stethoscope"></i>
            <h2 class="font-bold">{numberFormat.format(data.recovered)}</h2>
            <p class="text-2xl">Recuperados</p>
          </div>
          <p class="text-lg mt-5"><i>Hoy: +{numberFormat.format(data.todayRecovered)}</i></p>
        </article>
        <article class="bg-gray-500 p-6 rounded-lg shadow-inner">
          <div class="border-b pb-5">
            <i class="fas fa-skull-crossbones"></i>
            <h2 class="font-bold">{numberFormat.format(data.deaths)}</h2>
            <p class="text-2xl">Muertes</p>
          </div>
          <p class="text-lg mt-5"><i>Hoy: +{numberFormat.format(data.todayDeaths)}</i></p>
        </article>
      </div>
    </div>
    <div class="grid mt-8 px-6 divide-y md:grid-cols-4 md:py-6 md:px-0 md:divide-y-0 md:divide-x sm:mt-10 shadow-inner rounded-lg bg-gray-100">
      <div class="column py-6 md:py-0 md:px-6 md:divide-y">
        <div class="md:mb-6">
          <i class="fas fa-globe-americas"></i>
          <h3 class="my-1 font-bold">Países afectados</h3>
          <p>{numberFormat.format(data.affectedCountries)}</p>
        </div>
        {#each countries as {country}}
          <p class="py-6 italic hidden md:block truncate">{country}</p>
        {/each}
      </div>
      <div class="column py-6 md:py-0 md:px-6 md:divide-y">
        <div class="md:mb-6">
          <i class="fas fa-vial"></i>
          <h3 class="my-1 font-bold truncate">Pruebas Realizadas</h3>
          <p>{numberFormat.format(data.tests)}</p>
        </div>
        {#each countries as {tests}}
          <p class="py-6 italic hidden md:block">{numberFormat.format(tests)}</p>
        {/each}
      </div>
      <div class="column py-6 md:py-0 md:px-6 md:divide-y">
        <div class="md:mb-6">
          <i class="fas fa-head-side-virus"></i>
          <h3 class="my-1 font-bold">Casos Activos</h3>
          <p>{numberFormat.format(data.active)}</p>
        </div>
        {#each countries as {active}}
          <p class="py-6 italic hidden md:block">{numberFormat.format(active)}</p>
        {/each}
      </div>
      <div class="column py-6 md:py-0 md:px-6 md:divide-y">
        <div class="md:mb-6">
          <i class="fas fa-lungs-virus"></i>
          <h3 class="my-1 font-bold">En estado crítico</h3>
          <p>{numberFormat.format(data.critical)}</p>
        </div>
        {#each countries as {critical}}
          <p class="py-6 italic hidden md:block">{numberFormat.format(critical)}</p>
        {/each}
      </div>
    </div>
  {/await}
</section>