<script type="typescript">
	let numbers: Array<number> = [0, 0, 0, 0];
	let timeout: number = 500;
	let showTable: boolean = false;
	function generateRandomNumber(min: number, max: number) {
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
		min="100"
		max="10000"
		step="100"
	/>
	{timeout}ms
</p>
<button on:click={handleGoClick}>Go</button>
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
