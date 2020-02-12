<script>
	import { onMount } from 'svelte';
	import { mapbox } from './mapbox';

	let mapContainer;
	let map;
	let lat = 35;
	let lon = -84;
	let zoom = 3.5;

	onMount(() => {
		const link = document.createElement('link');
		link.rel = 'stylesheet';
		link.href = 'https://unpkg.com/mapbox-gl/dist/mapbox-gl.css';

		link.onload = () => {
			map = new mapbox.Map({
				container: mapContainer,
				style: 'mapbox://styles/mapbox/streets-v9',
				center: [lon, lat],
				zoom: zoom
			});
		};

		document.head.appendChild(link);

		return () => {
			map.remove();
			link.parentNode.removeChild(link);
		};
	});
</script>

<main>
	<div bind:this={mapContainer} class="map-container"></div>
</main>

<style>
	:global(body) {
		padding: 0px;
	}
	main {
		text-align: center;
		padding: 0px;
		width: 100%;
		height: 100vh;
		margin: 0 auto;
	}

	.map-container {
		width: 100%;
		height: 100vh;		
	}

</style>