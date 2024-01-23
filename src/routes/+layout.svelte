<script lang="ts">
	import '../app.css';
	import Error from './error/+page.svelte';
	import { page } from '$app/stores';
</script>

<svelte:head>
	<title>SvelteKit</title>
	<meta name="description" content="SvelteKit Template" />
	<link rel="icon" href="%sveltekit.assets%/favicon.png" />
</svelte:head>

<svelte>
	<div class="flex flex-col h-screen">
		<div class="flex flex-1 w-full">
			<div class="flex flex-col w-full">
				{#if $page.status != 404}
					<slot />
				{:else}
					<Error />
				{/if}
			</div>
		</div>
	</div>
</svelte>
