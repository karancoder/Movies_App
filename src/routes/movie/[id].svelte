<script context="module">
	export async function load({ fetch, params }) {
		const res = await fetch(
			`https://api.themoviedb.org/3/movie/${params.id}?api_key=${
				import.meta.env.VITE_API
			}&language=en-US`
		);
		const movieDetails = await res.json();
		console.log(movieDetails);
		if (res.ok) {
			return {
				props: { movieDetails }
			};
		}
		return {};
	}
</script>

<script>
	import { fly } from 'svelte/transition';
	export let movieDetails;
	export function printDate(date) {
		let dateObj = new Date(movieDetails.release_date);
		const monthNames = [
			'Jan',
			'Feb',
			'Mar',
			'Apr',
			'May',
			'Jun',
			'Jul',
			'Aug',
			'Sep',
			'Oct',
			'Nov',
			'Dec'
		];
		return dateObj.getDate() + ' ' + monthNames[dateObj.getMonth()] + ' ' + dateObj.getFullYear();
	}
	export function formatMoneyCount(count) {
		if (count < 1000) {
			return count;
		} else if (count < 1000000) {
			return Math.floor(count / 1000) + ' k';
		} else if (count < 1000000000) {
			return Math.floor(count / 1000000) + ' M';
		} else if (count < 1000000000000) {
			return Math.floor(count / 1000000000) + ' B';
		} else {
			return Math.floor(count / 1000000000) + ' T';
		}
	}
	export function formatVoteCount(voteCount) {
		return voteCount > 1000 ? Math.round(voteCount / 1000) + 'k' : voteCount;
	}
	export function printTime(time) {
		return time >= 60 ? Math.floor(time / 60) + ' hr ' + (time % 60) : time;
	}
</script>

<div
	class="movie-details"
	in:fly={{ y: 50, duration: 500, delay: 500 }}
	out:fly={{ duration: 500 }}
>
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
				{printDate(movieDetails.release_date)}
			</div>
			<div>
				<span>Rating: </span>
				{movieDetails.vote_average}/10 ({formatVoteCount(movieDetails.vote_count)} votes)
			</div>
			<div>
				<span>Budget: </span>
				{movieDetails.budget === 0 ? '-' : formatMoneyCount(movieDetails.budget)}
			</div>
			<div>
				<span>Runtime: </span>
				{printTime(movieDetails.runtime)} mins
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
		box-shadow: 3px 3px 5px rgba(0, 0, 0, 0.5);
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
