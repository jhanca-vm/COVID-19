<script>
	export let segment;
</script>

<style>
	[aria-current] {
		position: relative;
	}

	[aria-current]::after {
		position: absolute;
		content: '';
		width: 100%;
		height: 2px;
		background-color: #2c7a7b;
		display: block;
		bottom: -1.28rem;
		opacity: .25;
	}

	#logo::after {
		display: none;
	}

	@media screen and (min-width: 640px) {
		#down {
			display: none;
		}
	}
</style>

<header class="py-3 px-4 md:px-6 lg:px-8 shadow bg-gray-100">
	<div class="container mx-auto sm:flex sm:justify-between sm:items-center">
		<div class="flex items-center justify-between">
			<a id="logo" class="flex items-center justify-center" aria-current="{segment === undefined ? 'page' : undefined}" href=".">
				<img class="h-8" src="coronavirus.svg" alt="logo">
				<h1 class="ml-2 text-xl font-bold">COVID-19</h1>
			</a>
			<i id="down" class="ml-2 text-lg fas fa-chevron-down"></i>
		</div>
		<nav class="mt-2 hidden sm:block sm:mt-0">
			<ul class="flex justify-between">
				<li class="sm:mr-8 md:mr-12">
					<a aria-current="{segment === 'about' ? 'page' : undefined}" href="about">Países</a>
				</li>
				<li class="sm:mr-8 md:mr-12">
					<a rel=prefetch aria-current="{segment === 'blog' ? 'page' : undefined}" href="blog">Continentes</a>
				</li>
				<li>
					<p>Es <i class="fas fa-sort-down"></i></p>
				</li>
			</ul>
		</nav>
	</div>
</header>
