<script>
	import { onMount } from 'svelte';

	const carouselPhotos = [
		'https://cdn.pixabay.com/photo/2015/03/26/09/59/purple-690724_960_720.jpg',
		'https://cdn.pixabay.com/photo/2016/05/05/02/37/sunset-1373171_960_720.jpg',
		'https://cdn.pixabay.com/photo/2017/06/25/12/27/sunset-2440669_960_720.jpg'
	];

	let index = 0;

	const next = () => {
		index = (index + 1) % carouselPhotos.length;
	};

	onMount(() => {
		setInterval(() => {
		    next();
		}, 2000);
	});
</script>

<div class="slider relative">
	{#each [carouselPhotos[index]] as src (index)}
		<div class="alpha">
			<img class="img w-full h-80" {src} alt="" />
		</div>
		<div class="dots absolute flex bottom-6 w-full justify-center">
			{#each [0, 1, 2] as active}
				<div class="circle h-3 w-3 rounded-lg cursor-pointer my-0 mx-1 {active === index ? 'active' : ''}" />
			{/each}
		</div>
	{/each}
</div>

<style>
	.circle {
		background: #807676b5;
	}
	.active {
        @apply bg-white;
	}
</style>
