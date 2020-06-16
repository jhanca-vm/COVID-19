<script>
  import { onMount } from 'svelte';
  import Dashboard from '../components/Dashboard.svelte';

  let countries = [];

  onMount(async () => {
    const response = await fetch('https://corona.lmao.ninja/v2/countries?yesterday&sort');
    const data = await response.json();

    countries = data;
  });
</script>

<svelte:head>
  <title>COVID-19</title>
</svelte:head>

<Dashboard {countries}/>