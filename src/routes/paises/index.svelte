<script context="module">
	export async function preload() {
		const res = await this.fetch('https://corona.lmao.ninja/v2/countries?yesterday&sort');
		const countries = await res.json();

		return { countries };
	}
</script>

<script>
	import CountriesTable from "../../components/CountriesTable.svelte";
	
	export let countries;
</script>

<CountriesTable index="es" {countries}/>