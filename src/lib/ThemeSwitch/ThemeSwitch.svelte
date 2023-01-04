<script lang="ts">
	import { browser } from '$app/environment';

	let darkMode = true;
	let auto = true;

	function handleSwitchDarkMode() {
		darkMode = !darkMode;
		auto = false;
		localStorage.setItem('theme', darkMode ? 'dark' : 'light');

		if (darkMode) {
			document.documentElement.classList.add('dark');
			document.documentElement.classList.remove('light');
		} else {
			document.documentElement.classList.remove('dark');
			document.documentElement.classList.add('light');
		}
	}

	if (browser) {
		if (
			localStorage.theme === 'dark' ||
			(!('theme' in localStorage) && window.matchMedia('(prefers-color-scheme: dark)').matches)
		) {
			document.documentElement.classList.add('dark');
			document.documentElement.classList.remove('light');

			darkMode = true;
		} else {
			document.documentElement.classList.remove('dark');
			document.documentElement.classList.add('light');

			darkMode = false;
		}
	}

	function setAutoMode() {
		auto = true;
		localStorage.removeItem('theme');
		document.documentElement.classList.remove('dark');
		document.documentElement.classList.remove('light');
	}
</script>

<div>
	<span class="theme">Theme: {darkMode ? 'dark' : 'light'}</span>
	<span
		id="theme-toggle"
		class={darkMode ? 'dark' : 'light'}
		title="toggle light and dark-Mode"
		on:click={handleSwitchDarkMode}
		on:keydown={handleSwitchDarkMode}
	/>
</div>

<div>
	<span class="mode">Mode: {auto ? 'auto' : 'localStorage'}</span>

	<span id="auto" on:click={setAutoMode} on:keydown={setAutoMode} title="set to auto-Mode">
		<svg
			clip-rule="evenodd"
			fill-rule="evenodd"
			stroke-linejoin="round"
			stroke-miterlimit="2"
			viewBox="0 0 24 24"
			xmlns="http://www.w3.org/2000/svg"
			><path
				d="m3.508 6.726c1.765-2.836 4.911-4.726 8.495-4.726 5.518 0 9.997 4.48 9.997 9.997 0 5.519-4.479 9.999-9.997 9.999-5.245 0-9.553-4.048-9.966-9.188-.024-.302.189-.811.749-.811.391 0 .715.3.747.69.351 4.369 4.012 7.809 8.47 7.809 4.69 0 8.497-3.808 8.497-8.499 0-4.689-3.807-8.497-8.497-8.497-3.037 0-5.704 1.597-7.206 3.995l1.991.005c.414 0 .75.336.75.75s-.336.75-.75.75h-4.033c-.414 0-.75-.336-.75-.75v-4.049c0-.414.336-.75.75-.75s.75.335.75.75zm8.492 2.272c1.656 0 3 1.344 3 3s-1.344 3-3 3-3-1.344-3-3 1.344-3 3-3z"
				fill-rule="nonzero"
			/></svg
		></span
	>
</div>

<style>
	div {
		display: inline-flex;
		flex-direction: column;
		align-items: center;
		gap: 1rem;
		padding: 1rem;
		width: 3rem;
	}
	#theme-toggle {
		display: none;
	}

	#theme-toggle {
		display: inline-block;
		cursor: pointer;
		height: 3rem;
		width: 3rem;
		border-radius: 50%;
		transition: all 0.3s ease;
		content: '';
	}

	#theme-toggle.light {
		box-shadow: inset -18px -16px 1px 1px #fff;
	}

	#theme-toggle.dark {
		background-color: rgb(251 191 36);
	}

	#auto {
		display: inline-block;
		cursor: pointer;
		height: 3rem;
		width: 3rem;
		border-radius: 50%;
		border: none;
		background-color: transparent;
		content: '';
	}
</style>
