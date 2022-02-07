<script>
  import { form, field } from 'svelte-forms';
  import { required } from 'svelte-forms/validators';
  import { get } from 'svelte/store';
  
  const axieID = field('ID of Axie','',[required()]);
  const myForm = form(axieID);
  let axie, image;
  let parts = [];
  
  async function printCurrentValue() {
    const endpoint = "https://graphql-gateway.axieinfinity.com/graphql";
    const {value} = get(axieID);
    console.log(value);
    // ejemplo '8672514'
    const data = {
      operation: "GetAxieDetail",
      variables: {
	axieId: value
      },
      query: `query GetAxieDetail($axieId: ID!) {\n  axie(axieId: $axieId) {\n    ...AxieDetail\n    __typename\n  }\n}\n\nfragment AxieDetail on Axie {\n  id\n  image\n  class\n  chain\n  name\n  genes\n  owner\n  birthDate\n  bodyShape\n  class\n  sireId\n  sireClass\n  matronId\n  matronClass\n  stage\n  title\n  breedCount\n  level\n  figure {\n    atlas\n    model\n    image\n    __typename\n  }\n  parts {\n    ...AxiePart\n    __typename\n  }\n  stats {\n    ...AxieStats\n    __typename\n  }\n  auction {\n    ...AxieAuction\n    __typename\n  }\n  ownerProfile {\n    name\n    __typename\n  }\n  battleInfo {\n    ...AxieBattleInfo\n    __typename\n  }\n  children {\n    id\n    name\n    class\n    image\n    title\n    stage\n    __typename\n  }\n  __typename\n}\n\nfragment AxieBattleInfo on AxieBattleInfo {\n  banned\n  banUntil\n  level\n  __typename\n}\n\nfragment AxiePart on AxiePart {\n  id\n  name\n  class\n  type\n  specialGenes\n  stage\n  abilities {\n    ...AxieCardAbility\n    __typename\n  }\n  __typename\n}\n\nfragment AxieCardAbility on AxieCardAbility {\n  id\n  name\n  attack\n  defense\n  energy\n  description\n  backgroundUrl\n  effectIconUrl\n  __typename\n}\n\nfragment AxieStats on AxieStats {\n  hp\n  speed\n  skill\n  morale\n  __typename\n}\n\nfragment AxieAuction on Auction {\n  startingPrice\n  endingPrice\n  startingTimestamp\n  endingTimestamp\n  duration\n  timeLeft\n  currentPrice\n  currentPriceUSD\n  suggestedPrice\n  seller\n  listingIndex\n  state\n  __typename\n}\n`
    };
    try {
      const response = await fetch(endpoint, {
	method: 'POST',
	body: JSON.stringify(data),
	headers: {
      	  'content-type': 'application/json'
  	}
      });
      axie = await response.json();
      console.log(axie);
      image = axie.data.axie.image;
      parts = axie.data.axie.parts;
      console.log("Las partes ")
      for(let i = 0; i < parts.length; i++) {
	// https://loadedgamer.com/axie-body-parts-list/
	console.log(parts[i].id)
      }
    }
    catch(err) {
      console.log(err);
    }

  }

</script>

<main>
  <div class="col">
	<div class="img-thumbnail">
	<img class="img-thumbnail" src={image} alt="Foto de tu axie">
	<ul class="list-group">
	  {#each parts as part}
	    <li class="list-group-item"> {part.id} </li>
	  {/each} 
	</ul>
	</div>
      <section>
	<input type="number" bind:value={$axieID.value}>
	{#if $myForm.hasError('axieID.required')}
	  <p>The Axie ID is required</p>
	{/if}
	<button on:click={printCurrentValue}>Check for axie</button>
      </section>
  </div>
</main>
