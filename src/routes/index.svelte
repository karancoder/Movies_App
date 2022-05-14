<script context="module">
	export async function load({ fetch }) {
		const res = await fetch(
			`https://api.themoviedb.org/3/movie/popular?api_key=b5bc75631810aa3e97c310dfa067d9b0&language=en-US&page=1`
		);
		const data = await res.json();
		console.log(data);
		if (res.ok) {
			return {
				props: { popular: data.results }
			};
		}
	}
</script>

<script>
	import PopularMovies from './../components/PopularMovies.svelte';
	export let popular;
</script>

<section>
	<PopularMovies {popular} />
</section>
