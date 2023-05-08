<script type="ts">
	import { Button, ButtonGroup, Heading, P } from 'flowbite-svelte';
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher<{change: number}>();

	export let score = 1;

	function change(s: number) {
		score = s;
		dispatch('change', score);
	}

	export let question: string;
</script>

<div class="flex items-center gap-4 flex-wrap justify-between">
	<P class="mb-2">{question}</P>
	<ButtonGroup>
		{#each [1, 2, 3, 4, 5] as s}
        <Button on:click={() => change(s)} color={score === s ? 'purple' : 'light'}>{s}</Button>
        {/each}
	</ButtonGroup>
</div>
