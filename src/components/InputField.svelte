<script>
	let inputValue = '';
	let timer;

	let fetchData = null;

	const searchData = async () => {
		fetchData = null;
		if (inputValue.length > 3) {
			const res = await fetch(`https://pokeapi.co/api/v2/${inputValue}`);
			fetchData = await res.json();
		}
	};

	const handleSearch = async () => {
		clearTimeout(timer);
		timer = setTimeout(() => {
			searchData();
		}, 450);
	};
</script>

<div class="p-4">
	<div class="input-field">
		<input
			type="text"
			placeholder="Search name..."
			bind:value={inputValue}
			on:input={handleSearch}
			class="shadow outline-none w-full pl-2 py-2 border rounded border-grey-500 focus:border-blue-500 "
		/>
	</div>
	<div class="fetch-data mt-4">
		{#if fetchData}
			<ul>
				{#each fetchData.results as item}
					<li class="my-2 px-4 py-2 text-gray-600 text-sm border rounded border-grey-500">
						{item.name}
					</li>
				{/each}
			</ul>
		{:else}
			<p class="font-mono text-sm ml-3">Data not found...</p>
		{/if}
	</div>
</div>
