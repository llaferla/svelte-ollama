<script lang="ts">
	import ChatInput from './ChatInput.svelte';
    import ChatHistory from './ChatHistory.svelte';
</script>

<main>
	<ChatHistory />
	<ChatInput />
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>