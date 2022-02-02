<script>
  export let energy = 3;
  export let round = 1;
  function eraseEnergy() {
    if(energy > 0)
      energy--;
   
  }
  function endTurn() {
    energy+=2;
    round++;
  }
  function eraseAndGain() {
    energy--;
    energy++;
  }
  function reset() {
    energy = 3;
    round = 1;
  }
  function gainEnergy() {
    energy++;
  }
</script>
<main>
  <h2>Round {round}</h2>
  <h3> Energy: {energy} </h3>
  <div class="column">
    <span>
      <button on:click={eraseEnergy}>
	Used
      </button>
    </span>
    <span>
      <button on:click={eraseAndGain}>
	Energy Destroyed
      </button>
    </span>
    <span>
      <button on:click={gainEnergy}>
	Gain
      </button>
    </span>
    <span>
      <button on:click={endTurn}>
	End Turn
      </button>
    </span>
    <span>
      <button on:click={reset}>
	Reset
      </button>
    </span>
  </div>
</main>

<style>
  :root {
    --nord0: #2e3440;
    --nord1: #3b4252;
    --nord2: #434c5e;
    --nord3: #4c566a;
    --nord4: #d8dee9;
    --nord5: #e5e9f0;
    --nord6: #eceff4;
    --nord7: #8fbcbb;
    --nord8: #88c0d0;
    --nord9: #81a1c1;
    --nord10: #5e81ac;
    --nord11: #bf616a;
    --nord12: #d08770;
    --nord13: #ebcb8b;
    --nord14: #a3be8c;
    --nord15: #b48ead;
  }
  .column {
    display: flex;
    flex-direction: column;
    flex-basis: 3em;
  }
  button {
    height: 75px;
    width: 100px;
    text-align: center;
    background-color: var(--nord8);
    color: var(--nord3);
    box-shadow: 10px 5px var(--nord3);
  }
  button:hover {
    background-color: var(--nord9);
  }
  button:onClick {
    background-color: var(--nord4);
  }
  h2 {
    font-family: Roboto;
    font-weight: normal;
    color: var(--nord2);
  }

</style>
