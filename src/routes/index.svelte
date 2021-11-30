<script type="typescript">
	let numbers: Array<number> = [0, 0, 0, 0];
	let showNumbers: boolean = false;

	let timeout: number = 1000;
	let timeoutSeconds: number;
	$: timeoutSeconds = Number((timeout / 1000).toFixed(1));

	let rotate: boolean = false;
	let rotation: number = 0;
	let move: boolean = false;
	let xPos: number = 0;
	let yPos: number = 0;

	let alwaysShowNumbers: boolean = false;

	function generateRandomNumber(min: number, max: number): number {
		return Math.floor(Math.random() * (max - min + 1)) + min;
	}
	function handleGoClick() {
		for (let i = 0; i < numbers.length; i++) {
			numbers[i] = generateRandomNumber(0, 9);
		}
		showNumbers = true;
		rotation = rotate ? generateRandomNumber(-45, 45) : 0;
		xPos = move ? generateRandomNumber(-15, 20) : 0;
		yPos = move ? generateRandomNumber(-20, 20) : 0;
		setTimeout(() => (showNumbers = false), timeout);
	}
</script>

<main>
	<header>
		<h1>Memory Game</h1>
	</header>
	<section class="controls">
		<p>
			<span class="nowrap">Show numbers for:</span>
			<input
				id="timeoutSlider"
				bind:value={timeout}
				type="range"
				min="500"
				max="5000"
				step="500"
			/>
			<span class="nowrap">{timeoutSeconds} seconds</span>
		</p>
		<p>
			<input type="checkbox" bind:checked="{rotate}"/> rotate
			<input type="checkbox" bind:checked="{move}"/> move
			<input type="checkbox" bind:checked="{alwaysShowNumbers}"/> always show numbers
		</p>
	</section>
	<section class="numbers">
		{#if showNumbers || alwaysShowNumbers}
			<div id="numberValue" style="position: relative; left: {xPos}vw; top: {yPos}vh; transform: rotate({rotation}deg)">
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
	h1 {
		margin-bottom: 0;
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
		letter-spacing: 1.5rem;
		text-align: center;
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

	.nowrap {
		white-space: nowrap;
	}
</style>
