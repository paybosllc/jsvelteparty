<svelte:head>
	<title>J-Board</title>
	<meta name="description" content="JBoard Page" />

</svelte:head>

<script>
	import { onMount } from 'svelte';
	import ToggleCell from './ToggleCell.svelte';
	import { scoreTeamA, scoreTeamB, gameCategories, numberOfQuestions } from './store';

	/**
	 * @type {string | any[]}
	 */
	let titles = []; // = ['Title 1', 'Title 2', 'Title 3', 'Title 4', 'Title 5', ]
	/**
	 * @type {string}
	 */
	let categories;
	/**
	 * @type {number}
	 */
	let questions;
	/**
	 * @type {number}
	 */
	let teamAValue;
	/**
	 * @type {number}
	 */
	let teamBValue;

	gameCategories.subscribe((/** @type {any} */ value) => { categories = value})
	numberOfQuestions.subscribe(value => { questions = value})
	scoreTeamA.subscribe(value => { teamAValue = value})
	scoreTeamB.subscribe(value => { teamBValue = value})

	/**
	 * @param {string | number} number
	 */
	function doColumnUpdate(number) {
		const gridDiv = document.getElementById("myGridId");
		gridDiv?.style.setProperty('grid-template-columns', 'repeat(' + number + ', 1fr)')
	};

	onMount(() => {
		doColumnUpdate(titles.length);
		scoreTeamA.set(0);
		scoreTeamB.set(0);
		titles = categories.split(",");
		doColumnUpdate(titles.length);
	})

</script>

<div>
	<div class="mygrid" id="myGridId">
		<!-- place the categorie titles -->
		{#each titles as title}
			<h2 class="h2">{title}</h2>
		{/each}

		<!-- create the game board -->
		{#each Array(questions) as _, row(row)}
			{#each Array(titles.length) as _, col (col)}
				<ToggleCell scoreValue={(row + 1) * 200}/>
			{/each}
		{/each}
	</div>

	<div class="scoregrid">
		<h3 class="scorecard">Team A: {teamAValue}</h3>
		<h3 class="scorecard">Team B: {teamBValue}</h3>
	</div>
</div>

<style>

.mygrid {
	--columns: ;
	--rows: ;
	display: grid;
	grid-template-columns: repeat(var(--columns), 1fr);
	grid-template-rows: repeat(var(--rows), 1fr);
	grid-column-gap: 40px;
	grid-row-gap: 40px;
	margin: auto;
	justify-content: center;
	align-content: center;
	/* align-items: center; */
	text-align: center;
}

.h2 {
	color: aliceblue;
	font-size: 48px;
	font-weight: bold;
}

.scoregrid {
	display: grid;
	grid-template-columns: repeat(2, 1fr);
	grid-template-rows: repeat(1, 1fr);
	grid-column-gap: 80px;
	/* grid-row-gap: 40px; */
	margin: auto;
	justify-content: center;
	align-content: center;
	/* align-items: center; */
	text-align: center;
}

.scorecard {
	color: aliceblue;
	font-size: 52px;
	font-weight: bold;
}
</style>