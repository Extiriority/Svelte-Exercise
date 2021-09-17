<script lang="ts">
	import {SvelteComponent} from "svelte";
	import Nested from './Nested.svelte';
	import Info from './Info.svelte';

	export let name: string;

	let count = 0;
	$: doubled = count * 2;
	function incrementCount(){
		count += 1
	}

	$: if (count >= 10) {
		alert(`count is dangerously high!`);
		count = 0;
	}

	let numbers = [1, 2, 3, 4];

	function addNumber() {
		//numbers.push(numbers.length + 1);
		//numbers = numbers;
		numbers = [...numbers, numbers.length + 1]; //idiomatic way
		//numbers[numbers.length] = numbers.length + 1;
	}
	$: sum = numbers.reduce((previous, current) => previous + current);

	const pkg = {
		name: 'svelte',
		version: 3,
		speed: 'blazing',
		website: 'https://svelte.dev'
	};
</script>

<main>
	<h1>Hello {name.toUpperCase()}!</h1>
	<p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p>
	
	<button on:click={incrementCount}> clicked {count} {count === 1 ? 'time' : 'times'}</button>
	<p>{count} doubled is {doubled}</p>

	
	<button on:click={addNumber}>
		Add a number
	</button>
	<p>{numbers.join(' + ')} = {sum}</p>

	<Nested answer={42}/>
	<Nested/>

	<Info {...pkg}></Info>
</main>



<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>