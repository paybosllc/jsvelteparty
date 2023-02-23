
<script>
	import { createEventDispatcher } from 'svelte';
	const dispatch = createEventDispatcher();
	/**
	 * @type {string}
	 */
	 export let title;
	 /**
	 * @type {number}
	 */
	  export let score;
	 /**
	 * @type {boolean}
	 */
	  export let disabled;
	  /**
	 * @type {boolean}
	 */
	   export let selected;

	   function handleClick() {
		selected = !selected
		const scoreChange = selected ? score : -score;
	   	dispatch('scoreEvent', { text: title, value: scoreChange })
	  }

</script>

<div class="container">

<div class="cat action">
	<label>
	   <input type="checkbox" value="1" disabled={disabled} on:click={handleClick}><span>{title}</span>
	</label>
 </div>
</div>
<style>

.container {
	width: 40;
	height: 20;
	margin: auto;
}

.cat {
  margin: 4px;
  background-color: #104068;
  border-radius: 4px;
  border: 0px solid #fff;
  overflow: hidden;
  float: left;
}

.cat label {
  float: left; line-height: 3.0em;
  width: 4.0em; height: 3.0em;
}

.cat label span {
  font-weight: bold;
  font-size: 20px;
  text-align: center;
  padding: 0;
  display: block;
}

.cat label input {
  position: absolute;
  display: none;
  color: aliceblue;
}
/* selects all of the text within the input element and changes the color of the text */
.cat label input + span{color: #fff;}

/* This will declare how a selected input will look giving generic properties */
.cat input:checked + span {
    color: aliceblue;
    text-shadow: 0 0  6px rgba(0, 0, 0, 0.8);
}

.action input:checked + span{background-color: #FCAE1E;}
.action input:disabled + span {background-color: #BBBBBB; }

</style>
