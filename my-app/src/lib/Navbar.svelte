<script>
	import { goto } from '$app/navigation';
	import user from '../user';
	$: isLoggedIn = $user === null ? false : true;

	const logout = () => {
		// Here logout endpoint would need to be added when available
		user.update((val) => (val = null));
		isLoggedIn = false;
		goto('/login', { noScroll: false, replaceState: true });
	};
</script>

<nav class="navbar">
	<a class="nav_link" href="/">Home</a>
	{#if isLoggedIn === false}
		<a class="nav_link" href="/login">Login</a>
	{:else}
		<button
			class="nav_btn"
			on:click={logout}
			style="display; transparent; padding: 0;
    background: none;">Logout</button
		>
	{/if}
</nav>

<style>
	.navbar {
		display: flex;
		flex-direction: row;
		align-items: center;
		position: absolute;
	}
	.nav_link {
		text-decoration: none;
		font-size: 1.25em;
		color: #fc521a;
		margin: 0 1em;
	}

	.nav_btn {
		text-decoration: none;
		font-size: 1.25em;
		color: #fc521a;
		margin: 0 1em;
		border: none;
	}
	.nav_link:hover {
		border-bottom: 2px solid #fc521a;
	}

	.nav_btn:hover {
		border-bottom: 2px solid #fc521a;
		cursor: pointer;
	}
</style>
