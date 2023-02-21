<svelte:head>
	<title>Settings</title>
	<meta name="description" content="Game Settings" />
</svelte:head>

<script>
	import { gameCategories, numberOfQuestions } from '../store';

	/**
	 * @type {string}
	 */
	let categories;
	/**
	 * @type {number}
	 */
	let questions;

	categories = "";
	questions = 5;

	gameCategories.subscribe((/** @type {any} */ value) => { categories = value})
	numberOfQuestions.subscribe(value => { questions = value})

	let textBoxEntries = categories.split(",");
	const numbers = [4, 5, 6];

	function saveSettings() {
		const csvString = textBoxEntries.join(',');
		gameCategories.set(csvString);
		numberOfQuestions.set(questions)
	}

</script>

<div class="text-column">

	<h1>Settings</h1>
	  <h3>Categories:</h3>
	  {#each textBoxEntries as entry, i}
		<input class="textentry" type="text" bind:value={textBoxEntries[i]} />
	  {/each}

	  <h3>Number of Questions</h3>
	  <select class="opt" bind:value={questions}>
		{#each numbers as number}
			<option class="opt" value={number}>{number}</option>
		{/each}
	  </select>

	  <div class="container">
		  <button class="but" on:click={saveSettings}>Save Settings</button>
	  </div>
<!--
	  <p>
		This is a long string to help with padding, why do I need this silly thing...
	  </p>
 -->
	</div>

<style>

.opt {
	margin: 10px;
	padding: 10px;
	height: 50px;
	width: 50%;
	font-size: large;
}

.but {
	padding: 10px;
	font-size: large;
	font-weight: bold;
}

.container {
	display: flex;
	margin: 40px;
	justify-content: center;
	align-items: center;
}

.textentry {
	padding: 10px;
	margin: 10px;
}

</style>
