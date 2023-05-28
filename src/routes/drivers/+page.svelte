<script>
// @ts-nocheck

	import axios from "axios";
    import Navbar from "../../components/Navbar.svelte";
	import { onMount } from 'svelte';
    axios.defaults.baseURL = 'http://localhost:8080';
    import { Popover, Button } from 'flowbite-svelte'
    import { slide } from 'svelte/transition';
    import { Table, TableBody, TableBodyCell, TableBodyRow, TableHead, TableHeadCell } from 'flowbite-svelte';

    /**
	 * @type {any[]}
	 */
    let drivers = [];
    let firstName = '';
    let lastName = '';
    let phoneNumber = '';
    let email = '';
    let showForm = false;

    async function getDrivers(){
        try{
            const response = await axios.get('/driver');
            drivers = response.data;
        }catch(error){
            console.error(error);
        }
    }

    async function addNewDriver(){
        try{
            const response = await axios.post('/driver', {
                firstName, 
                lastName, 
                phoneNumber, 
                email
            });
            getDrivers();
            firstName = '';
            lastName = '';
            phoneNumber = '';
            email = '';
            showForm = false;
        }catch(error){
            console.error(error);
        }
    }

    onMount(() => {
        getDrivers();
    })
</script>

<Navbar />
<div class="w-2/3 mx-auto bg-gray-300 rounded-lg">
      <Table striped={true}>
        <TableHead>
          <TableHeadCell>First Name</TableHeadCell>
          <TableHeadCell>Last Name</TableHeadCell>
          <TableHeadCell>Phone Number</TableHeadCell>
          <TableHeadCell>Email</TableHeadCell>
          <TableHeadCell>
            <span class="sr-only">Edit</span>
          </TableHeadCell>
        </TableHead>
        <TableBody class="divide-y">
          {#each drivers as driver}
            <TableBodyRow>
              <TableBodyCell>{driver.firstName}</TableBodyCell>
              <TableBodyCell>{driver.lastName}</TableBodyCell>
              <TableBodyCell>{driver.phoneNumber}</TableBodyCell>
              <TableBodyCell>{driver.email}</TableBodyCell>
              <TableBodyCell>
                <div class = "flex justify-end">
                  <Button color = "blue" style="margin-right: 0.5rem;">Edit</Button>
                  <Button color = "red" style="margin-right: 0.5rem;">Delete</Button>
                </div>
              </TableBodyCell>
            </TableBodyRow>
          {/each}
        </TableBody>
      </Table>
</div>

<div class="text-center mt-4">
  <Button color="green" on:click={() => showForm = true}>Add New Driver</Button>
  <Popover class="w-64 text-sm font-light" title="New Driver" transition={slide}>
    {#if showForm}
    <form on:submit|preventDefault={addNewDriver}>
      <label for="firstName">First Name:</label>
      <input type="text" id="firstName" bind:value={firstName} required />

      <label for="lastName">LastName:</label>
      <input type="text" id="lastName" bind:value={lastName} required />

      <label for="phoneNumber">Phone Number:</label>
      <input type="tel" id="phoneNumber" bind:value={phoneNumber} required />

      <label for="email">Email:</label>
      <input type="email" id="email" bind:value={email} required />

      <Button color="green" style="margin-right: 0.5rem; margin-top: 0.5rem; padding: 0.5rem 1rem; font-size: 0.8rem;">Save</Button>
    </form>
    {/if}
  </Popover>
</div>