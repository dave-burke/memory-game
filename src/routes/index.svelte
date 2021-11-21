<script type="typescript">
	let numbers: Array<number> = [0, 0, 0, 0];
	let timeout: number = 500;
	let showTable: boolean = false;
	let timeoutSeconds: number;
	$: timeoutSeconds = Number((timeout / 1000).toFixed(1));
	function generateRandomNumber(min: number, max: number): number {
		return Math.floor(Math.random() * (max - min + 1)) + min;
	}
	function handleGoClick() {
		for (let i = 0; i < numbers.length; i++) {
			numbers[i] = generateRandomNumber(0, 9);
			showTable = true;
			setTimeout(() => (showTable = false), timeout);
		}
	}
</script>

<h1>Memory Game</h1>
<p>
	Show numbers for: <input
		id="timeoutSlider"
		bind:value={timeout}
		type="range"
		min="500"
		max="5000"
		step="500"
	/>
	{timeoutSeconds} seconds
</p>
<!-- autofocus is only an a11y problem in conditionally rendered elements-->
<!-- https://github.com/sveltejs/svelte/issues/6629#issuecomment-894803517 -->
<!-- svelte-ignore a11y-autofocus -->
<button on:click={handleGoClick} autofocus>Go</button>
{#if showTable}
	<table>
		<tbody>
			<tr>
				<td>{numbers[0]}</td>
				<td>{numbers[1]}</td>
				<td>{numbers[2]}</td>
				<td>{numbers[3]}</td>
			</tr>
		</tbody>
	</table>
{/if}

<style>
	#timeoutSlider {
		width: 20rem;
	}
	button {
		width: 10rem;
		padding: 2rem;
		font-size: larger;
		font-weight: bold;
	}
	table {
		margin-left: auto;
		margin-right: auto;
	}
	table td {
		padding: 2rem;
		font-size: xx-large;
		font-weight: bold;
	}
</style>
