<script lang="ts">
	import { onMount } from 'svelte';

    let items = [];
    let nonFilteredItems = [];
    let item = null;
    let index = null;

    const findItem = (catagory: string) => {
        items = nonFilteredItems.filter(v => v.catagory === catagory);
        index = Math.floor(Math.random() * items.length);
        item = items[index];
    }

	onMount(() => {
        console.log("mount");
		items = JSON.parse(localStorage.getItem('items')) || [];
        nonFilteredItems = items;

        let urlparams = new URLSearchParams(window.location.search);
        let cat = urlparams.get('cat');
        if (cat) {
            findItem(cat);
        }

        index = Math.floor(Math.random() * items.length);
        item = items[index];
	});
</script>

<h1 class="text-2xl text-center pt-3 pb-4">Let's get it done!</h1>

{#if items.length === 0}
    <div class="text-xl text-center">No tasks found. <a href="/new">Create your first task</a></div>
{:else}
    <!-- <div class="text-2xl text-center p-1">Task</div> -->
    <div class="text-3xl text-center p-2"><span class="p-1">{item.title}</span> - <a href={`/workon?task=${index}`} class="rounded border-grey-200 p-1">Do it</a></div>
    <div class="text-center pt-4">Or <a href="/new">create another task</a></div>
    <div class="text-center">Or pick a catagory</div>
    <div class="text-sm text-center">
        {#each [...new Set(nonFilteredItems.map(v => v.catagory))] as catagory}
            <a class="p-1" href={`/?cat=${catagory}`} on:click="{() => findItem(catagory)}">{catagory}</a>
        {/each}
    </div>
{/if}
