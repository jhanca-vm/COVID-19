<script>
  import Dashboard from '../components/Dashboard.svelte';

  let index = 'es';
</script>

<svelte:head>
  <title>COVID-19</title>
</svelte:head>

<Dashboard {index}/>
