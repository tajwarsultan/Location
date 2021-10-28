<script>
	export let distanInKm;
</script>

<div
	class="distane-model absolute top-20 left-1/4 right-1/4
        bg-gray-100
        p-10 rounded-md 
        flex justify-center items-center "
>
	{#if distanInKm}
		<h3 class="italic">
			<span class="font-semibold"> Distance:</span>
			{distanInKm} km
		</h3>
	{/if}
</div>
