<script>
	import Navbar from "../../components/Navbar.svelte";
</script>

<Navbar />
<div class="container mx-auto px-4">
	<h1 class="text-4xl font-bold mb-8">Make a new reservation</h1>

	<div class="grid grid-cols-1 md:grid-cols-2 gap-8">
		<!-- Driver Information -->
		<div class="bg-white rounded-md shadow-md p-6">
			<h2 class="text-lg font-bold mb-4">Driver Information</h2>
			<form>
				<div class="mb-4">
					<label class="block font-bold mb-2" for="first-name">First Name:</label>
					<input
						class="border border-gray-300 p-2 w-full rounded-md"
						type="text"
						id="first-name"
						name="first-name"
						placeholder="Enter the first name"
					/>
				</div>

				<div class="mb-4">
					<label class="block font-bold mb-2" for="last-name">Last Name:</label>
					<input
						class="border border-gray-300 p-2 w-full rounded-md"
						type="text"
						id="last-name"
						name="last-name"
						placeholder="Enter the last name"
					/>
				</div>

				<div class="mb-4">
					<label class="block font-bold mb-2" for="phone-number">Phone Number:</label>
					<input
						class="border border-gray-300 p-2 w-full rounded-md"
						type="tel"
						id="phone-number"
						name="phone-number"
						placeholder="Enter the phone number"
					/>
				</div>

				<div class="mb-4">
					<label class="block font-bold mb-2" for="email">Email:</label>
					<input
						class="border border-gray-300 p-2 w-full rounded-md"
						type="email"
						id="email"
						name="email"
						placeholder="Enter the email"
					/>
				</div>
			</form>
		</div>

		<!-- Location -->
		<div class="bg-white rounded-md shadow-md p-6">
			<h2 class="text-lg font-bold mb-4">Location</h2>
			<form>
				<div class="mb-4">
					<label class="block font-bold mb-2" for="address">Address:</label>
					<div class="relative">
						<select
							class="border border-gray-300 p-2 w-full rounded-md appearance-none"
							id="address"
							name="address"
						>
						</select>
						<div
							class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-2 text-gray-700"
						>
							<svg
								class="fill-current h-4 w-4"
								xmlns="http://www.w3.org/2000/svg"
								viewBox="0 0 20 20"
								><path
									d="M14.707 7.293a1 1 0 0 0-1.414-1.414L10 8.586 6.707 5.293a1 1 0 0 0-1.414 1.414l3.292 3.292a1 1 0 0 0 1.414 0l3.292-3.292a1 1 0 0 0 0-1.414z"
								/></svg
							>
						</div>
					</div>
				</div>

				<div class="mb-4">
					<label class="block font-bold mb-2" for="gate">Gate:</label>
					<div class="relative">
						<select
							class="border border-gray-300 p-2 w-full rounded-md appearance-none"
							id="gate"
							name="gate"
						>
						</select>
						<div
							class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-2 text-gray-700"
						>
							<svg
								class="fill-current h-4 w-4"
								xmlns="http://www.w3.org/2000/svg"
								viewBox="0 0 20 20"
								><path
									d="M14.707 7.293a1 1 0 0 0-1.414-1.414L10 8.586 6.707 5.293a1 1 0 0 0-1.414 1.414l3.292 3.292a1 1 0 0 0 1.414 0l3.292-3.292a1 1 0 0 0 0-1.414z"
								/></svg
							>
						</div>
					</div>
				</div>
			</form>
		</div>
	</div>
</div>

<div class="text-center mt-4">
	<button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
		Submit
	</button>
</div>

