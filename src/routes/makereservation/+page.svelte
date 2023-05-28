<script>
	import axios from 'axios';
	import {onMount} from 'svelte';
	import { each } from 'svelte/internal';
	import Navbar from '../../components/Navbar.svelte';
  import { Button } from 'flowbite-svelte';

	let driverId = 0;
	/**
	 * @type {any[]}
	 */
	let drivers = [];

	let locationId = 0;
	/**
	 * @type {any[]}
	*/
	let locations = [];
  /**
   * @type {any[]}
   */
  let statuses = [];
  let status = '';

  let dispatchDate = '';
  let deliveryDate = '';
  let deliveryHour = '';

	async function getDrivers(){
		try{
			const response = await axios.get('http://localhost:8080/driver', {
			});
			drivers = response.data;
		}catch(error){
			console.error(error);
		}
	}

  async function getLocations(){
    try{
			const response = await axios.get('http://localhost:8080/location', {
			});
			locations = response.data;
		}catch(error){
			console.error(error);
		}
	}

  async function getStatuses(){
    try {
    const response = await axios.get('http://localhost:8080/transport/status');
    statuses = response.data;
  } catch (error) {
    console.error(error);
  }
  }

  async function addTransport() {
      try{
        const response = await axios.post('http://localhost:8080/transport', {
          driverId,
          locationId,
          status,
          dispatchDate,
          deliveryDate,
          deliveryHour
        });
        console.log(response.data);
      }catch (error){
        console.error(error);
      }
    }

	onMount(() => {
		getDrivers();
    getLocations();
    getStatuses();
	})
</script>

<Navbar />
<body class="bg-gray-100">
    <div class="flex items-center justify-center min-h-screen">
      <div class="w-1/2 p-8">
        <div class="mb-4">
          <label for="driver" class="block text-gray-700 font-bold mb-2">Driver</label>
          <select class="block w-full py-2 px-3 border border-gray-300 bg-white rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500" id="driver" bind:value={driverId}>
            {#each drivers as driver}
				<option value = {driver.driverId}>{driver.firstName} {driver.lastName}</option>
			{/each}
          </select>
        </div>

        <div class="mb-4">
          <label for="location" class="block text-gray-700 font-bold mb-2">Location</label>
          <select class="block w-full py-2 px-3 border border-gray-300 bg-white rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500" id = "location"bind:value={locationId}>
            {#each locations as location}
              <option value={location.locationId}>{location.address}</option>
            {/each}
          </select>
        </div>

        <div class="mb-4">
          <label for="status" class="block text-gray-700 font-bold mb-2">Status</label>
          <select id="status" name = "status" class="block w-full py-2 px-3 border border-gray-300 bg-white rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500" bind:value={status}>
            {#each statuses as statusOption}
              <option value = { statusOption }>{ statusOption }</option>
            {/each}
          </select>
        </div>

        <div class="mb-4">
          <label for="dispatch-date" class="block text-gray-700 font-bold mb-2">Dispatch Date</label>
          <input id="dispatch-date" name="dispatch-date" type="date" class="block w-full py-2 px-3 border border-gray-300 bg-white rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500" bind:value={dispatchDate}>
        </div>

        <div class="mb-4">
          <label for="delivery-date" class="block text-gray-700 font-bold mb-2">Delivery Date</label>
          <input id="delivery-date" name="delivery-date" type="date" class="block w-full py-2 px-3 border border-gray-300 bg-white rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500" bind:value={deliveryDate}>
        </div>

        <div class="mb-4">
          <label for="delivery-hour" class="block text-gray-700 font-bold mb-2">Delivery Hour</label>
          <input
            id="delivery-hour"
            name="delivery-hour"
            type="time"
            class="block w-full py-2 px-3 border border-gray-300 bg-white rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500"
            bind:value={deliveryHour}
          />
        </div>

        <div class="flex justify-center">
          <Button color = "green" style="margin-right: 0.5rem;" on:click={addTransport}>Submit</Button>
        </div>
      </div>
    </div>
</body>