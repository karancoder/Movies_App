<script>
	export let popular;
	import MoviesCard from './MoviesCard.svelte';
</script>

<h2>Popular Movies</h2>

<div class="popular-movies">
	{#each popular as movie}
		<MoviesCard {movie} />
	{/each}
</div>

<style>
	h2 {
		padding: 0 1rem;
		font-weight: 800;
	}

	.popular-movies {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
		grid-column-gap: 1rem;
		grid-row-gap: 2rem;
	}
</style>
