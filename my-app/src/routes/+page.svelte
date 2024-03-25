<script>
	import { onMount } from 'svelte';
	import user from '../user';

	let wholeuser = null;
	user.subscribe((prevValue) => (wholeuser = prevValue));
	$: isLoggedIn = $user === null ? false : true;
	// onMount(async()=>{
	//     const userLoggedInStatus = async()=>{
	//         const result = await fetch('http://localhost:3030/api/user',{
	//             method: 'GET',
	//             credentials: 'include',
	//             headers: {
	//                 'Accept': 'application/json',
	//                 'content-type': 'application/json'
	//             }
	//         })
	//         return result
	//     }
	//     const result = await userLoggedInStatus();
	//     const returnedData = await result.json();
	//     if(returnedData.success === true) user.update(val => val = returnedData.data)
	// })

	console.log('user', user);
</script>

<div class="content_wrapper">
	{#if isLoggedIn}
		<h3>Welcome back to Childhood.</h3>
		<h4>Thank you for logging in, {$user.name}</h4>
	{:else}
		<h4>You need to be logged in to enter.</h4>
		<h4>Head to Login page above.</h4>
	{/if}
</div>

<style>
	/* h1, h2{
        color: black;
    } */
	.content_wrapper {
		margin-top: 4em;
		text-align: center;
		color: white;
	}
</style>
