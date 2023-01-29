<script lang="ts">
    import type { ActionData } from './$types'

export let form: ActionData
</script>

<h1>Register</h1>


<form action="?/register" method ="POST">
    <div>
        <label for="username" placeholder="enter username">username</label>
        <input id="username"  name="username" type="text" required>
    </div>
    <div>
        <label for="username" placeholder="enter password">username</label>
        <input id="password"  name="password" type="password" required>
    </div>
<button type="submit">Register</button>
</form>

{#if form?.user}
<p class="error">Username is taken</p>
{/if}