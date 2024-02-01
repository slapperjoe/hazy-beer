<script>
	import { fade } from 'svelte/transition';
	import milk from '$lib/images/milk-plant.webp';

	let milky = false;
	setTimeout(()=>{milky = true;}, 3000)
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Hazy Beer" />
</svelte:head>

<section>
	<img src={milk} alt="Metal Plant"/>
	<h1>
		Hazy beer.
	</h1>
	{#if milky}
		<h2 transition:fade={{duration: 2000}}>
			Just go get a milkshake instead.
		</h2>   
	{/if}


</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
	}

	h1 {
		width: 100%;
	}

	h2 {
		margin-top: -14px;
	}

</style>
