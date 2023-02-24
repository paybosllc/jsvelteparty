
<script>
	import TCell from './TCell.svelte';
  import ToggleButton from './ToggleButton.svelte'
  import { scoreTeamA, scoreTeamB } from './store'
  import { writable } from 'svelte/store'

  $: showToggle = false
  $: tbASelected = false
  $: tbBSelected = false

  /**
	 * @type {number}
	 */
   export let scoreValue;

  function scoreEvent(e) {
    if (e.detail.text === 'A') {
      $scoreTeamA += e.detail.value
    }
    else {
      $scoreTeamB += e.detail.value
    }
  }

</script>

<div class="container" id="gridId">
{#if !showToggle}
<div>
  <button class="no-border" on:click|preventDefault={() => showToggle = !showToggle}>{scoreValue}</button>
</div>
{:else}
<div>
  <TCell>
    <ToggleButton title='A' score={scoreValue} disabled={tbBSelected} bind:selected={tbASelected} on:scoreEvent={scoreEvent} />
    <ToggleButton title='B' score={scoreValue} disabled={tbASelected} bind:selected={tbBSelected} on:scoreEvent={scoreEvent} />
  </TCell>
</div>
{/if}
</div>

<style>

.no-border {
  background: #4040FF;
  color: #FCAE1E;
  border: none;
  font-size: 60px;
  font-weight: bold;
}

.container {
	display: grid;
	grid-template-columns: repeat(1, 1fr);
	grid-template-rows: repeat(0, 1fr);
	grid-column-gap: 10px;
	grid-row-gap: 0px;
	margin: auto;
}

</style>
