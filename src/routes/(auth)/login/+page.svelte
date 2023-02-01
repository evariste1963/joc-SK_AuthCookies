<script lang="ts">
	//import { fail } from '@sveltejs/kit';
	import { applyAction, enhance } from '$app/forms'
	import { invalidateAll } from '$app/navigation';
	import type { ActionData } from './$types';

	export let form: ActionData;
</script>

<h1>Login</h1>

<form action="?/login" method="POST" use:enhance={() => {
	return async ({ result }) => {
		//rerun the 'load' function for the page
		//https://kit.svelte.dev.docs.modules#app-navigation-invalidateall
		invalidateAll()

		//since we are customizng the default behavior
		//we don't want to reimplpement what 'use:enhance' does
		//so we can use 'applyresult' and pass the 'result'
		await applyAction(result)
	}
}}>
	<div>
		<label for="username">username</label>
		<input id="username" name="username" type="text" data-required="true" />
	</div>
	<div>
		<label for="password">password</label>
		<input id="password" name="password" type="password" data-required="true" />
	</div>

	{#if form?.invalid}
		<p class="error">Username and password required</p>
	{/if}

	{#if form?.credentials}
		<p class="error">You have entered the wrong username or password</p>
	{/if}
	<button type="submit">Log in</button>
</form>
