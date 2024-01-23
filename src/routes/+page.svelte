<script lang="ts">
	import Button from '../components/Button/Button.svelte';
	import Counter from '../components/Counter/Counter.svelte';

	interface CounterItem {
		inputValue: string;
		count: number;
	}

	let counters: CounterItem[] = [{ inputValue: 'new', count: 0 }];

	const addCounter = () => {
		counters = [...counters, { inputValue: 'new', count: 0 }];
	};

	const increaseCount = (index: number) => {
		counters[index].count += 1;
	};

	const decreaseCount = (index: number) => {
		if (counters[index].count - 1 < 0) return;
		counters[index].count -= 1;
	};

	const initCount = (index: number) => {
		counters[index].count = 0;
	};

	$: titleList = counters.map((counter) => counter.inputValue).join(', ');
	$: sumOfCount = counters.reduce((sum, counter) => sum + counter.count, 0);
</script>

<div class="flex flex-col justify-center items-center h-screen gap-4">
	<div class="flex flex-col items-center justify-center w-full text-white text-5xl">
		Multiple Counter
	</div>

	<div class="flex flex-col gap-4">
		{#each counters as counter, index}
			<Counter
				key={index}
				bind:counter
				increase={() => increaseCount(index)}
				decrease={() => decreaseCount(index)}
				init={() => initCount(index)}
				remove={(indexToRemove) => {
					counters = counters.filter((_, currentIndex) => currentIndex !== indexToRemove);
				}}
			/>
		{/each}
		<Button label="New Counter" onClick={addCounter} color="bg-red-100" />
	</div>

	<div class="flex flex-row gap-2">
		<span class="text-white">Title list:</span>
		<span class="text-white"> {titleList}</span>
	</div>
	<div class="flex flex-row gap-2">
		<span class="text-white">Sum of count:</span>
		<span class="text-white">{sumOfCount}</span>
	</div>
</div>
