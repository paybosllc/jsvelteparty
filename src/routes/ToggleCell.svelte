
<script>
	import TCell from './TCell.svelte';
  import ToggleButton from './ToggleButton.svelte'
  import { scoreTeamA, scoreTeamB } from './store'

  let showToggle = false;
  let tbASelected = false;
  let tbBSelected = false;

  /**
	 * @type {number}
	 */
   export let scoreValue;

  function doToggle() {
    showToggle = !showToggle
  }

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
<div>
  <button class:hide={showToggle} class="no-border" on:click={doToggle}>{scoreValue}</button>
</div>

<div class:hide={!showToggle}>
  <TCell>
    <ToggleButton title='A' score={scoreValue} disabled={tbBSelected} bind:selected = {tbASelected} on:scoreEvent={scoreEvent} />
    <ToggleButton title='B' score={scoreValue} disabled={tbASelected} bind:selected = {tbBSelected} on:scoreEvent={scoreEvent} />
  </TCell>
</div>
</div>

<style>

.hide {
  display: none;
}

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
