<script>
	import Header from '../components/Header.svelte';

	export let segment;
</script>

<style>
	:global(body) {
		font-family: 'Lato', sans-serif;
		color: #2d3748;
	}

	@keyframes -global-rotate {
    from {
      transform: rotate(0deg);
    }
    to {
      transform: rotate(360deg);
    }
  }
</style>

<Header {segment}/>
<main class="px-4 py-6 sm:px-4 md:px-6 lg:px-8 lg:pt-8">
	<slot></slot>
</main>