<script lang="ts">
	import { applyAction, enhance } from '$app/forms';
	import { invalidateAll } from '$app/navigation';
	import { page } from '$app/stores';
	import '../styles/app.css';
</script>

<svelte:head>
	<title>SvelteKit Auth</title>
</svelte:head>

<nav>
	{#if !$page.data.user}
	{#if !$page.url.pathname.startsWith('/login')}
		<a href="/login">Login</a>
		{/if}
		{#if !$page.url.pathname.startsWith('/register')}
		<a href="/register">Register</a>
		{/if}
	{/if}

	{#if $page.data.user}
		<!-- hide ADMIN button when in admin -->
		{#if !$page.url.pathname.startsWith('/admin')}
			<a href="/admin">Admin</a>
		{/if}
		<form
			class="logout"
			action="/logout"
			method="POST"
			use:enhance={() => {
				return async ({ result }) => {
					//rerun the 'load' function for the page
					//https://kit.svelte.dev.docs.modules#app-navigation-invalidateall
					invalidateAll();

					//since we are customizng the default behavior
					//we don't want to reimplpement what 'use:enhance' does
					//so we can use 'applyresult' and pass the 'result'
					await applyAction(result);
				};
			}}
		>
			<button type="submit">Log out</button>
		</form>
	{/if}
</nav>

<main>
	<slot />
</main>
