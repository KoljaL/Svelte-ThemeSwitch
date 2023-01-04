<script lang="ts">
	import ThemeSwitch from '$lib/ThemeSwitch/ThemeSwitch.svelte';

	import '../app.css';
</script>

<div class="wrapper">
	<ThemeSwitch />
	<h1>Theme Switch</h1>
</div>

<style>
	.wrapper {
		display: flex;
		flex-direction: row;
		align-items: center;
	}
	h1 {
		color: var(--color-text);
		margin: 5rem;
	}
</style>
