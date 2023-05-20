<script>
    import { Navbar, NavBrand, NavLi, NavUl, NavHamburger } from 'flowbite-svelte';
    import Logo from './drxlogo.svg'

</script>

<Navbar let:hidden let:toggle color="form">
    <NavBrand href="/homepage">
      <img
        src={Logo}
        class="mr-3 h-6 sm:h-9"
        alt="Draxlmaier Logo"
      />
      
    </NavBrand>
    <NavHamburger on:click={toggle} />
    <NavUl {hidden}>
      <NavLi href="/homepage" active={true}>Home</NavLi>
      <NavLi href="/addemployees">Employees</NavLi>
      <NavLi href="/addlocations">Locations</NavLi>
      <NavLi href="/makereservation">Make reservation</NavLi>
      <NavLi href="/transports">Transports</NavLi>
    </NavUl>
  </Navbar>

  