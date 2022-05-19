<script context="module">
	export async function load({ fetch, params }) {
		const res = await fetch(
			`https://api.themoviedb.org/3/search/movie?api_key=${
				import.meta.env.VITE_API
			}&language=en-US&query=${params.id}&page=1&include_adult=false&`
		);
		const data = await res.json();
		console.log(data);
		if (res.ok) {
			return {
				props: { searchedMovies: data.results }
			};
		}
		return {};
	}
</script>

<script>
	export let searchedMovies;
	import MoviesCard from './../../components/MoviesCard.svelte';
</script>

<div class="searched-movies">
	{#each searchedMovies as movie}
		<MoviesCard {movie} />
	{/each}
</div>

<style>
	.searched-movies {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
		grid-column-gap: 1rem;
		grid-row-gap: 2rem;
	}
</style>
