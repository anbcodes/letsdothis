<script lang="ts">
	import { onMount } from 'svelte';

    let items = [];
    let item = null;

	onMount(() => {
		items = JSON.parse(localStorage.getItem('items')) || [];

        let params = new URLSearchParams(location.search);

        item = items[params.get('task')];
	});
</script>



{#if !item}
<h1 class="text-xl text-red">Invaild Item</h1>
{:else}

<h1 class="text-2xl text-center pt-3 pb-4">Current Task</h1>
<div class="text-3xl text-center p-2"><span class="p-1">{item.title}</span></div>
<div class="text-center text-sm pt-4"> 
    <a href="/">&lt- back</a>
</div>
{/if}