<script context="module">
	export async function load({ fetch, params }) {
		const res = await fetch(
			`https://api.themoviedb.org/3/movie/${params.id}?api_key=b5bc75631810aa3e97c310dfa067d9b0&language=en-US`
		);
		const movieDetails = await res.json();
		console.log(movieDetails);
		if (res.ok) {
			return {
				props: { movieDetails }
			};
		}
	}
</script>

<script>
	export let movieDetails;
</script>

<div class="movie-details">
	<div class="img-container">
		<img
			src={'https://image.tmdb.org/t/p/original' + movieDetails.backdrop_path}
			alt="movieDetails.title"
		/>
	</div>
	<div class="data-container">
		<h1>{movieDetails.title}</h1>
		<div class="movie-numbers">
			<div>
				<span>Release Date: </span>
				{movieDetails.release_date}
			</div>
			<div>
				<span>Rating: </span>
				{movieDetails.vote_average} ({movieDetails.vote_count} votes)
			</div>
			<div>
				<span>Budget: </span>
				{movieDetails.budget}
			</div>
			<div>
				<span>Runtime: </span>
				{movieDetails.runtime} mins
			</div>
		</div>
		<p class="description">{movieDetails.overview}</p>
	</div>
</div>

<style>
	.movie-details {
		margin: 2rem 20%;
		display: flex;
		flex-direction: column;
		align-items: center;
	}

	h1 {
		margin: 0;
		padding: 1rem 0rem;
	}

	p {
		margin: 0;
		padding: 0.5rem 0;
	}

	.img-container {
		width: 100%;
	}

	img {
		width: 100%;
		border-radius: 1rem;
	}

	span {
		font-weight: bold;
	}

	.movie-numbers {
		margin: 0;
		padding: 0.5rem 0;
		display: grid;
		grid-template-columns: repeat(2, 1fr);
	}
</style>
