<script>
	import Navbar from '../lib/Navbar.svelte';
</script>

<div class="main-content">
	<Navbar />
	<slot />
</div>

<style>
	.main-content {
		display: flex;
		flex-direction: column;
		align-items: center;
		background-color: black;
		color: whitesmoke;
		font-weight: 100;
		font-family: fantasy;
	}
</style>
