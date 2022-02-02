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

  import {onMount} from "svelte";
  import axios from "axios";
  const endpoint = "https://jsonplaceholder.typicode.com/posts";
  let posts = [];
  onMount(async function () {
    const response = await fetch(endpoint);
    const data = await response.json;
    console.log("Hola");
    console.log(data);
  });
</script>

<main>
  <Navbar />
  <div>
  <EnergyCounter />
  </div>
  {#each posts as article}
  <div>
    <p>{article.title}</p>
  </div>
  {/each}
  <div>
    <DamageCalculator />
  </div>
</main>
