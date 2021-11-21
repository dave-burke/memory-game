<script type="typescript">
	let numbers: Array<number> = [0, 0, 0, 0];
	let timeout: number = 1000;
	let showNumbers: boolean = false;
	let timeoutSeconds: number;
	$: timeoutSeconds = Number((timeout / 1000).toFixed(1));
	function generateRandomNumber(min: number, max: number): number {
		return Math.floor(Math.random() * (max - min + 1)) + min;
	}
	function handleGoClick() {
		for (let i = 0; i < numbers.length; i++) {
			numbers[i] = generateRandomNumber(0, 9);
			showNumbers = true;
			setTimeout(() => (showNumbers = false), timeout);
		}
	}
</script>

<main>
	<header>
		<h1>Memory Game</h1>
	</header>
	<section class="controls">
		Show numbers for: <input
			id="timeoutSlider"
			bind:value={timeout}
			type="range"
			min="500"
			max="5000"
			step="500"
		/>
		{timeoutSeconds} seconds
	</section>
	<section class="numbers">
		{#if showNumbers}
			<div id="numberValue">
				{numbers[0]}
				{numbers[1]}
				{numbers[2]}
				{numbers[3]}
			</div>
		{/if}
	</section>

	<footer>
		<!-- autofocus is only an a11y problem in conditionally rendered elements-->
		<!-- https://github.com/sveltejs/svelte/issues/6629#issuecomment-894803517 -->
		<!-- svelte-ignore a11y-autofocus -->
		<button on:click={handleGoClick} autofocus>Go</button>
	</footer>
</main>

<style>
	main {
		height: 100%;
		margin-left: 2rem;
		margin-right: 2rem;
		display: flex;
		flex-direction: column;
	}
	section.numbers {
		flex: 1 0 auto;
		display: flex;
		flex-direction: column;
		justify-content: center;
	}
	.numbers {
		margin: auto;
		font-size: xx-large;
		font-weight: bold;
		letter-spacing: 2rem;
	}
	footer {
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 2rem;
	}
	#timeoutSlider {
		width: 20rem;
	}
	button {
		width: 10rem;
		padding: 2rem;
		font-size: larger;
		font-weight: bold;
	}
</style>
