<script>
	import { onMount } from 'svelte';

	let name;
	let command = '';
	let history = [];
	let cursorPosition = 0;

	onMount(() => {
		name = localStorage.getItem('name') || 'username';
		window.addEventListener('keydown', handleKey);
	});

	function handleKey(e) {
		if (e.key === 'Enter') {
			history.push(command);
			command = '';
			cursorPosition = 0;
		} else if (e.key === 'Backspace') {
			e.preventDefault();
			if (cursorPosition > 0) {
				command = command.slice(0, cursorPosition - 1) + command.slice(cursorPosition);
				cursorPosition--;
			}
		} else if (e.key === 'ArrowLeft') {
			if (cursorPosition > 0) cursorPosition--;
		} else if (e.key === 'ArrowRight') {
			if (cursorPosition < command.length) cursorPosition++;
		} else if (e.key.length === 1) {
			command = command.slice(0, cursorPosition) + e.key + command.slice(cursorPosition);
			cursorPosition++;
		}
	}
</script>

<div class="terminal">
	{#each history as entry}
		<p>{name}@tools:~$ {entry}</p>
	{/each}
	<div class="field">
		<p class="precursor">{name}@tools:~$</p>
		{#if command.length === 0}
			<span class="cursor"></span>
		{:else}
			{#each Array.from(command) as char, i}
				{#if i === cursorPosition}
					<span class="cursor"></span>
				{/if}
				<span>{char}</span>
			{/each}
			{#if cursorPosition === command.length}
				<span class="cursor"></span>
			{/if}
		{/if}
	</div>
</div>

<style lang="scss">
	:global(body) {
		background-color: #000;
		color: #fff;
		font-family: 'Cascadia Code', Consolas, 'Courier New', monospace;
		font-size: 16px;
		padding: 20px;
		white-space: pre-wrap;
	}

	.field {
		display: flex;
		flex-wrap: wrap;
		align-items: flex-end;
	}

	.precursor {
		margin: 0;
	}

	.cursor {
		display: inline-block;
		width: 8px;
		height: 1em;
		background-color: #fff;
		animation: blink 1s steps(1) infinite;
		margin-left: 1px;
	}

	@keyframes blink {
		0%,
		49% {
			opacity: 1;
		}
		50%,
		100% {
			opacity: 0;
		}
	}
</style>
