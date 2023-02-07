<script>
	// import Header from './Header.svelte';
	import Nested from './Nested.svelte';
	import './styles.css';
	let name = 'world';
	let src = 'src/lib/images/svelte-welcome.png';
	let string = `this string contains some <strong>HTML!!!</strong>`;
	let count = 0;
	$: doubled = count * 2;

	$: if (count >= 10) {
		alert('count is dangerously high!');
		count = 9;
	}

    function incrementCount() {
        count += 1;
    }
	let numbers = [1, 2, 3, 4];

	function addNumber() {
		// numbers.push(numbers.length + 1);
		// numbers = numbers;
		numbers = [...numbers, numbers.length + 1];
	}

	$: sum = numbers.reduce((t, n) => t + n, 0);
	import Info from './Info.svelte';

	const pkg = {
		name: 'svelte',
		version: 3,
		speed: 'blazing',
		website: 'https://svelte.dev'
	};
	let user = { loggedIn: false };

	function toggle() {
		user.loggedIn = !user.loggedIn;
	}
	let x = 7;
</script>

<div class="app">
	<!-- <Header /> -->

	<main>
		<h1>Hello {name}!</h1>
		<img src={src} alt="A man dances.">
		<p>This is a paragraph.</p>
		<Nested answer={55}/>
		<Nested/>
		<p>{@html string}</p>
		<button on:click={incrementCount}> 	Clicked {count} {count === 1 ? 'time' : 'times'} </button>
	    <p>{count} doubled is {doubled}</p>

		<p>{numbers.join(' + ')} = {sum}</p>

		<button on:click={addNumber}>
			Add a number
		</button>
		<Info name={pkg.name} version={pkg.version} speed={pkg.speed} website={pkg.website}/>
		{#if user.loggedIn}
			<button on:click={toggle}>
				Log out
			</button>
		{:else}
			<button on:click={toggle}>
				Log in
			</button>
		{/if}
		{#if x > 10}
			<p>{x} is greater than 10</p>
		{:else}
			{#if 5 > x}
				<p>{x} is less than 5</p>
			{:else}
				<p>{x} is between 5 and 10</p>
			{/if}
		{/if}
	</main>

	<footer>
		<p>visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to learn SvelteKit</p>
	</footer>
</div>

<style>
	.app {
		display: flex;
		flex-direction: column;
		min-height: 100vh;
	}

	main {
		flex: 1;
		display: flex;
		flex-direction: column;
		padding: 1rem;
		width: 100%;
		max-width: 64rem;
		margin: 0 auto;
		box-sizing: border-box;
	}

	footer {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		padding: 12px;
	}

	footer a {
		font-weight: bold;
	}

	@media (min-width: 480px) {
		footer {
			padding: 12px 0;
		}
	}

	p {
		color: purple;
		font-family: 'Comic Sans MS', cursive;
		font-size: 2em;
	}
</style>
