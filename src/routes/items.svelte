<script lang="ts">
	import { onMount } from 'svelte';

    let items = [];

	onMount(() => {
		items = JSON.parse(localStorage.getItem('items')) || [];
	});
</script>

<h1 class="text-2xl text-center">Your items</h1>

{#each items as item}
<div class="text-xl text-center">
    <h2>{item.title}</h2>
    <p>{item.catagory}</p>
    <input type="checkbox" bind:value={item.completed}>
</div>
{/each}