<script lang="ts">
	import type { ActionData } from './$types';

	export let form: ActionData;
</script>

<h1>Register</h1>

<form action="?/register" method="POST">
	<div>
		<label for="username" placeholder="enter username">username</label>
		<input id="username" name="username" type="text" data-required="true" />
	</div>
	<div>
		<label for="password" placeholder="enter password">password</label>
		<input id="password" name="password" type="password" data-required="true" />
	</div>

	{#if form?.user}
		<p class="error">Username is taken</p>
	{/if}

	<button type="submit">Register</button>
</form>
