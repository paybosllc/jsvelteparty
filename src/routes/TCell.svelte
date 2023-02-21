<div class="tcell">
	<slot></slot>
</div>

<style>
.tcell {
	display: grid;
	grid-template-columns: repeat(2, 1fr);
	grid-template-rows: repeat(0, 1fr);
	grid-column-gap: 0px;
	grid-row-gap: 0px;
	margin: auto;
}
</style>