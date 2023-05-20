<script>
	import axios from 'axios';
	import { onMount } from 'svelte';
	import { createEventDispatcher } from 'svelte';
	axios.defaults.baseURL = 'http://localhost:8080';
	import Navbar from '../../components/Navbar.svelte';
	import { token } from '../auth';



	let address = '';
	let locationId = 0;
	/**
	 * @type {any[]}
	 */
	let locations = [];

	const dispatch = createEventDispatcher();

	async function addLocation() {
		try {
			const response = await axios.post('/location', { address });
			console.log(response.data);
			locations = [...locations, response.data];
			locationId = response.data.location_id;
			address = '';
		} catch (error) {
			console.error(error);
		}
	}

	async function addGate() {
		try {
			const response = await axios.post('/gate', { locationId });
			console.log(response.data);
			dispatch('gateAdded');
		} catch (error) {
			console.error(error);
		}
	}

	async function getLocations() {
		try{
			const response = await axios.get('/location', {
				headers : {
					Authorization: `Bearer ${token}`,
				},
			});
			locations = response.data;
		}catch (error){
			console.error(error);
		}
	}

	onMount(() => {
		getLocations();
	});
</script>

<Navbar />
<div class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
	<h2 class="text-xl font-bold mb-4">Add Location</h2>
	<div class="mb-4">
		<label class="block text-gray-700 font-bold mb-2" for="address"> Address </label>
		<input
			class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
			id="address"
			type="text"
			placeholder="Enter the address"
			bind:value={address}
		/>
	</div>
	<div class="text-center mt-4">
		<button
			on:click={addLocation}
			class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
			type="button"
		>
			Add Location
		</button>
	</div>
</div>

<div class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
	<h2 class="text-xl font-bold mb-4">Add Gate</h2>
	<div class="mb-4">
		<label class="block text-gray-700 font-bold mb-2" for="location"> Location </label>
		<select
			class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
			id="location"
			bind:value={locationId}
		>
			{#each locations as location}
				<option value={location.locationId}>{location.address}</option>
			{/each}
		</select>
	</div>
	<div class="text-center mt-4">
		<button
			on:click={addGate}
			class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
			type="button"
		>
			Add Gate
		</button>
	</div>
</div>
