<script>
  const API = 'https://corona.lmao.ninja/v2/all?yesterday';
  
  async function getData() {
    const response = await fetch(API);
    const data = await response.json();
    return data;
  };
</script>

<section class="container mx-auto">
  {#await getData()}
    loading...
  {:then data}  
    <div class="text-gray-100 text-5xl">
      <div class="grid sm:grid-cols-2 lg:grid-cols-3 gap-6">
        <article class="bg-red-500 p-6 rounded-lg text-center shadow-inner">
          <div class="border-b pb-5">
            <i class="fas fa-viruses"></i>
            <h2 class="font-bold">{data.cases.toLocaleString()}</h2>
            <p class="text-2xl">Casos</p>
          </div>
          <p class="text-lg mt-5"><i>Hoy: +{data.todayCases}</i></p>
        </article>
        <article class="bg-teal-500 p-6 rounded-lg text-center shadow-inner">
          <div class="border-b pb-5">
            <i class="fas fa-stethoscope"></i>
            <h2 class="font-bold">{data.recovered.toLocaleString()}</h2>
            <p class="text-2xl">Recuperados</p>
          </div>
          <p class="text-lg mt-5"><i>Hoy: +{data.todayRecovered}</i></p>
        </article>
        <article class="bg-gray-500 p-6 rounded-lg text-center shadow-inner">
          <div class="border-b pb-5">
            <i class="fas fa-skull-crossbones"></i>
            <h2 class="font-bold">{data.deaths.toLocaleString()}</h2>
            <p class="text-2xl">Muertes</p>
          </div>
          <p class="text-lg mt-5"><i>Hoy: +{data.todayDeaths}</i></p>
        </article>
      </div>
    </div>
    <div class="grid px-6 divide-y md:grid-cols-4 md:py-6 md:px-0 md:divide-y-0 md:divide-x text-center mt-10 shadow-inner rounded-lg bg-gray-100">
      <div class="py-6 md:p-0">
        <i class="fas fa-globe-americas"></i>
        <h3>Países afectados</h3>
        <p>{data.affectedCountries.toLocaleString()}</p>
      </div>
      <div class="py-6 md:p-0">
        <i class="fas fa-vial"></i>
        <h3>Pruebas Realizadas</h3>
        <p>{data.tests.toLocaleString()}</p>
      </div>
      <div class="py-6 md:p-0">
        <i class="fas fa-head-side-virus"></i>
        <h3>Casos Activos</h3>
        <p>{data.active.toLocaleString()}</p>
      </div>
      <div class="py-6 md:p-0">
        <i class="fas fa-lungs-virus"></i>
        <h3>En estado crítico</h3>
        <p>{data.critical.toLocaleString()}</p>
      </div>
    </div>
  {/await}
</section>