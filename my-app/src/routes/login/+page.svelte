<script>
	import { goto } from '$app/navigation';

	import { error } from '@sveltejs/kit';
	import user from '../../user';

	let userCode = '';
	let password = '';

	let errorMessage = null;
	let status = null;

	// original url to be used when accessing without proxy:
	// 'http://10.2.2.10/AlbiScanner.stage/api/v1/login',
	const login = () => {
		fetch('http://localhost:8010/proxy', {
			method: 'POST',
			headers: {
				'Content-Type': 'application/json'
			},
			body: JSON.stringify({ userCode: userCode, password: password })
		})
			.then((res) => res.json())
			.then((data) => {
				if (data?.messages?.length === 0 && !data?.errors) {
					alert('You are successfully logged in!');
					goto('/', { noScroll: false, replaceState: true });
					user.update((val) => (val = data.user));
				}
				// here is handling of an error with a message attribute,
				// which only error object has (case when no entry is given)
				else if (data?.message) {
					errorMessage = data?.errors[0]?.messages[0];
				} else {
					if (data?.user) {
						alert(data.messages[0].content);
						goto('/', { noScroll: false, replaceState: true });

						user.update((val) => (val = data.user));
					} else {
						errorMessage = data?.messages[0].content;
					}
				}
			})
			.catch((err) => {
				// just to make sure also other error types are caught here
				console.log('Error logging in:', err);
				alert(err.message);
			});
	};
</script>

<div
	style="display: flex; justify-content: space-around;
	 flex-flow: column; margin-top: 65px"
>
	<h3 style="text-align: center; font-weight: normal; opacity: 0.9;">
		„Hra je jeden z nejefektivnějších způsobů, jak zjednodušit život.
		<br />Přesně to jsme dělali jako děti, ale v dospělosti jsme si hrát zapomněli.“ A.E.
	</h3>
	<form on:submit|preventDefault={login} style="text-align: center; background-color:black">
		<div>
			<label style="font-weight: lighter;" for="userCode">User code</label>
			<input
				autocomplete="off"
				type="text"
				id="userCode"
				bind:value={userCode}
				style="text-align: center; background-color:black;
				color:antiquewhite; border-radius: 10px"
			/>
		</div>
		<div>
			<label style="font-weight: lighter;" for="password">Password</label>
			<input
				autocomplete="off"
				type="password"
				id="password"
				bind:value={password}
				style="text-align: center; background-color:black;
				color:antiquewhite; border-radius: 10px;"
			/>
		</div>
		{#if errorMessage}
			<p style="color: #fc521a; font-size:small; margin-bottom: 0px">
				{errorMessage}
			</p>
		{/if}
		<button
			type="submit"
			style="cursor:pointer;  border-radius: 10px; 
			width: 20%; text-align:center; margin: 10px 50%;
			font-family: inherit; font-weight: lighter;">Enter</button
		>
	</form>
</div>
