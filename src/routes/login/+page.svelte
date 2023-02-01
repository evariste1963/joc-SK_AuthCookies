<script lang="ts">
	//import { fail } from '@sveltejs/kit';

	import type { ActionData } from './$types';

	export let form: ActionData;
</script>

<h1>Login</h1>

<form action="?/login" method="POST">
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
