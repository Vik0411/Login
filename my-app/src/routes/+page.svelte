<script>
	import user from '../user';

	let wholeUser = null;
	user.subscribe((prevValue) => (wholeUser = prevValue));
	$: isLoggedIn = $user === null ? false : true;
	// Here onMount would normally eventually be used
	// for getting the logged-in user

	console.log('userObject', user);
</script>

<div class="content_wrapper">
	{#if isLoggedIn}
		<h3 style="font-weight: lighter;">Welcome back to Childhood.</h3>
		<h4 style="font-weight: lighter;">Thank you for logging in, {$user.name}</h4>
	{:else}
		<h4 style="font-weight: lighter;">You need to be logged in to enter.</h4>
		<h4 style="font-weight: lighter;">Head to Login page above.</h4>
	{/if}
</div>

<style>
	.content_wrapper {
		margin-top: 4em;
		text-align: center;
		color: white;
	}
</style>
