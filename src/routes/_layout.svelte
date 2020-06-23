<script>
	import Header from '../components/Header.svelte';

	export let segment;
</script>

<style>
	:global(body) {
		font-family: 'Lato', sans-serif;
		color: #e6fffa;
		background-color: #285e61;
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
<main class="px-4 my-5 sm:px-4 md:px-6 lg:px-8 lg:py-6">
	<slot></slot>
</main>