<script>
	let options = {
		enableHighAccuracy: true,
		timeout: 5000,
		maximumAge: 0
	};

	let distanInKm = 0;
	let popup = false;

	const toRad = (degrees) => {
		return degrees * (Math.PI / 180);
	};

	const onGeoSuccess = (postion) => {
		const radiusOfEarth = 6371;
		const userLat = postion.coords.latitude;
		const userLon = postion.coords.longitude;
		const bermudaTriangleLat = 25.0;
		const bermudaTriangleLon = 71.0;
		var dLat = toRad(bermudaTriangleLat - userLat);
		var dLon = toRad(bermudaTriangleLon - userLon);
		var a =
			Math.sin(dLat / 2) * Math.sin(dLat / 2) +
			Math.cos(toRad(userLat)) *
				Math.cos(toRad(bermudaTriangleLat)) *
				Math.sin(dLon / 2) *
				Math.sin(dLon / 2);
		var c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1 - a));
		const distance = radiusOfEarth * c;
		distanInKm = distance.toFixed(2);
	};

	const onGeoError = (error) => {
		console.log({ error });
	};
	const getLocation = () => {
		let geolocation = navigator.geolocation;
		if (geolocation) {
			geolocation.getCurrentPosition(onGeoSuccess, onGeoError, options);
		}
		popup = !popup;
	};
	import DistanModel from './DistanModel.svelte';
</script>

<div class="user-location p-4 flex justify-center items-center w-full">
	<button
		class="bg-grey-600 
               border-2 border-blue-600 rounded-md px-16 py-3"
		on:click={getLocation}>Get Distance</button
	>
	{#if popup}
		<DistanModel {distanInKm} />
	{/if}
</div>
