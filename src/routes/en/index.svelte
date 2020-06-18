<script>
  import Dashboard from '../../components/Dashboard.svelte';

  let index = 'en';
</script>

<svelte:head>
  <title>COVID-19</title>
</svelte:head>

<Dashboard {index}/>