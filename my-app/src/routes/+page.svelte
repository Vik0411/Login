<script>
    import {onMount} from 'svelte';
    import user from '../user';

    let wholeuser = null
    user.subscribe(prevValue => wholeuser = prevValue)
    $: isLoggedIn = $user===null ? false : true;
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

console.log("user", user)

</script>

<div class="content_wrapper">
    <h1>Welcome back to Childhood.</h1>
    {#if isLoggedIn}
    <h2>Thank you for logging in {$user}</h2>
    {:else}
    <h2>You need to be logged in here.</h2>
    <h2>Head to Sign in page above</h2>
    {/if}
</div>

<style>
    h1, h2{
        color: black;
    }
    .content_wrapper{
        margin-top: 4em;
        text-align: center;
    }
</style>