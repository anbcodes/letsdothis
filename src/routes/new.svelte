<script lang="ts">
	import { onMount } from 'svelte';

	let items = [];

	let title = '';
	let catagory = '';

	let catagories = [];

	onMount(() => {
		items = JSON.parse(localStorage.getItem('items')) || [];
		catagories = [...new Set(items.map((v) => v.catagory))];
	});

	const create = () => {
		items.push({
			title,
			catagory,
			completed: false
		});
		localStorage.setItem('items', JSON.stringify(items));
		title = '';
		catagory = '';
		window.location.pathname = '/';
	};
</script>

<h1 class="text-2xl text-center">What do you need to do?</h1>
<div class="flex justify-center">
	<div class="lg:w-1/3 flex flex-col">
		<input class="m-2 p-1 rounded border border-gray-500" type="text" bind:value={title} />
		<div class="text-sm m-2 flex justify-center">
			<div class="w-2/3">
				<span class="mr-2">Catagory</span>
				<input
					class="rounded border p-1 border-gray-500"
					list="suggestions"
					bind:value={catagory}
				/>
				<datalist id="suggestions">
					{#each catagories as catagory}
						<option value={catagory} />{/each}
				</datalist>
			</div>
		</div>
		<div class="flex justify-center">
			<button
				class="m-2 p-1 w-1/2 text-xl rounded-lg border border-gray-500 hover:bg-gray-100"
				on:click={create}>Do it!</button
			>
		</div>
	</div>
</div>
