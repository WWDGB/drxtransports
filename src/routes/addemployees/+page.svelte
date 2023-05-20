<script>
	import axios from 'axios';
	import { onMount } from 'svelte';
	import Navbar from '../../components/Navbar.svelte';

	axios.defaults.baseURL = 'http://localhost:8080';

	let firstName = '';
	let lastName = '';
	let phoneNumber = '';
	let email = '';
	let locationId = 0;
	/**
	 * @type {any[]}
	 */
	let locations = [];

	async function addEmployee() {
		try {
			const response = await axios.post('/employee', {
				firstName,
				lastName,
				phoneNumber,
				email,
				locationId
			});
			console.log(response.data);
		} catch (error) {
			console.error(error);
		}
	}

	onMount(async () => {
		const response = await axios.get('/location');
		locations = response.data;
	});
</script>

<Navbar />
<div class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4 flex flex-col my-2">
	<form>
		<div class="-mx-3 md:flex mb-6">
			<div class="md:w-1/2 px-3 mb-6 md:mb-0">
				<label
					class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2"
					for="first_name"
				>
					First Name
				</label>
				<input
					class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
					id="first_name"
					type="text"
					placeholder="Enter the first name"
					bind:value={firstName}
				/>
			</div>
			<div class="md:w-1/2 px-3">
				<label
					class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2"
					for="last_name"
				>
					Last Name
				</label>
				<input
					class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
					id="last_name"
					type="text"
					placeholder="Enter the last name"
					bind:value={lastName}
				/>
			</div>
		</div>
		<div class="-mx-3 md:flex mb-6">
			<div class="md:w-1/2 px-3">
				<label
					class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2"
					for="phone_number"
				>
					Phone Number
				</label>
				<input
					class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
					id="phone_number"
					type="tel"
					placeholder="Enter the phone number"
					bind:value={phoneNumber}
				/>
			</div>
			<div class="md:w-1/2 px-3">
				<label
					class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2"
					for="email"
				>
					Email
				</label>
				<input
					class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
					id="email"
					type="email"
					placeholder="Enter the email"
					bind:value={email}
				/>
			</div>
		</div>
		<div class="-mx-3 md:flex mb-6">
			<div class="md:w-1/2 px-3 mb-6 md:mb-0">
				<label
					class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2"
					for="location"
				>
					Location
				</label>
				<div class="relative">
					<select
						class="appearance-none block w-full bg-gray-200 border border-gray-200 text-gray-700 py-3 px-4 pr-8 rounded leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
						id="location"
						bind:value={locationId}
					>
						{#each locations as location}
							<option value={location.locationId}>{location.address}</option>
						{/each}
					</select>
					<div
						class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-2 text-gray-700"
					>
						<svg
							class="fill-current h-4 w-4"
							xmlns="http://www.w3.org/2000/svg"
							viewBox="0 0 20 20"
						>
							<path
								d="M14.95 7.95l-3.93 3.93c-.2.2-.5.2-.7 0l-3.93-3.93c-.2-.2-.2-.5 0-.7l.7-.7c.2-.2.5-.2.7 0l3.23 3.22 3.23-3.22c.2-.2.5-.2.7 0l.7.7c.2.2.2.5 0 .7z"
							/>
						</svg>
					</div>
				</div>
			</div>
		</div>
		<div class="text-center mt-4">
			<button
				class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
				type="button"
				on:click={addEmployee}
			>
				Add Employee
			</button>
		</div>
	</form>
</div>
