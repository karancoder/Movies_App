<script>
	let searchInputValue = '';
	import { fly } from 'svelte/transition';
	import { goto } from '$app/navigation/';
	function submitSearch() {
		goto('/search/' + searchInputValue);
	}
</script>

<form on:submit|preventDefault={submitSearch} class="search">
	<input
		bind:value={searchInputValue}
		class={`search-input ${searchInputValue ? '' : 'search-has-no-input'}`}
		type="text"
		placeholder="Search Movies"
		size="25"
	/>
	{#if searchInputValue}
		<button out:fly={{ y: 30, duration: 500 }} in:fly={{ y: -30, duration: 500 }} class="search-btn"
			>Search</button
		>
	{/if}
</form>

<style>
	form {
		display: flex;
		margin: 1rem;
	}

	form > * {
		border: none;
		padding: 0.7rem;
		font-size: 1rem;
		font-weight: bold;
	}

	.search-input {
		border-top-left-radius: 10px;
		border-bottom-left-radius: 10px;
	}

	.search-btn {
		color: white;
		background: rgb(206, 157, 241);
		border-top-right-radius: 10px;
		border-bottom-right-radius: 10px;
		cursor: pointer;
	}

	.search-has-no-input {
		border-top-right-radius: 10px;
		border-bottom-right-radius: 10px;
	}

	.search-input:focus {
		outline: none;
	}
</style>
