<svelte:head>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;700&display=swap" rel="stylesheet">

<style>
 main {
    text-align: center;
    background-color: var(--nord6);
  }

  h1 {
    font-family: Roboto;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: bold;
    color: var(--nord3);
  }
  #damageCalculator {
    display: flex;
    flex-direction: row;
  }
  @media (min-width: 640px) {
    main {
      max-width: none;
      grid-gap: 5% 90%;
    }
  }
</style>
</svelte:head>
<script>  
  import Navbar from './Navbar.svelte';
  import EnergyCounter from './Energy_Counter.svelte';
  import DamageCalculator from './DamageCalculator.svelte';
  import Activity from './Activity.svelte';
</script>

<main>
  <Navbar />
  <div id="#EnergyCounter">
  <EnergyCounter />
  </div>
  <br>
  <br>
  <br>
  <h1>Damage Calculator</h1>
  <div class="row align-items-center">
    <div class="col">
    <DamageCalculator />
    </div>
    <div class="col">
    <DamageCalculator />
    </div>
    <div class="col">
      <DamageCalculator />
    </div>
  </div>
  <div>
    <Activity />
  </div>
</main>
