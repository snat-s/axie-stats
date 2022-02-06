<script>
	import { onMount } from "svelte";
	const endpoint = "https://graphql-gateway.axieinfinity.com/graphql";
	let axie, image, clase;
	let parts = [];
	const data = {
  	operation: "GetAxieDetail",
  	variables: {
    	axieId: '8672514'
  	},
  	query: `query GetAxieDetail($axieId: ID!) {\n  axie(axieId: $axieId) {\n    ...AxieDetail\n    __typename\n  }\n}\n\nfragment AxieDetail on Axie {\n  id\n  image\n  class\n  chain\n  name\n  genes\n  owner\n  birthDate\n  bodyShape\n  class\n  sireId\n  sireClass\n  matronId\n  matronClass\n  stage\n  title\n  breedCount\n  level\n  figure {\n    atlas\n    model\n    image\n    __typename\n  }\n  parts {\n    ...AxiePart\n    __typename\n  }\n  stats {\n    ...AxieStats\n    __typename\n  }\n  auction {\n    ...AxieAuction\n    __typename\n  }\n  ownerProfile {\n    name\n    __typename\n  }\n  battleInfo {\n    ...AxieBattleInfo\n    __typename\n  }\n  children {\n    id\n    name\n    class\n    image\n    title\n    stage\n    __typename\n  }\n  __typename\n}\n\nfragment AxieBattleInfo on AxieBattleInfo {\n  banned\n  banUntil\n  level\n  __typename\n}\n\nfragment AxiePart on AxiePart {\n  id\n  name\n  class\n  type\n  specialGenes\n  stage\n  abilities {\n    ...AxieCardAbility\n    __typename\n  }\n  __typename\n}\n\nfragment AxieCardAbility on AxieCardAbility {\n  id\n  name\n  attack\n  defense\n  energy\n  description\n  backgroundUrl\n  effectIconUrl\n  __typename\n}\n\nfragment AxieStats on AxieStats {\n  hp\n  speed\n  skill\n  morale\n  __typename\n}\n\nfragment AxieAuction on Auction {\n  startingPrice\n  endingPrice\n  startingTimestamp\n  endingTimestamp\n  duration\n  timeLeft\n  currentPrice\n  currentPriceUSD\n  suggestedPrice\n  seller\n  listingIndex\n  state\n  __typename\n}\n`
	};
	onMount(async function () {
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
			clase = axie.data.axie.class;
			parts = axie.data.axie.parts;
			console.log("Las partes ")
			for(let i = 0; i < parts.length; i++) {
				// https://loadedgamer.com/axie-body-parts-list/
				console.log(parts[i].id)
			}
			fetch("https://axie-infinity.p.rapidapi.com/get-battle-log/0x519695110e22e0cd584cbdade2e71647b1f5a667", {
	"method": "GET",
	"headers": {
		"x-rapidapi-host": "axie-infinity.p.rapidapi.com",
		"x-rapidapi-key": "4e75ef97cbmsh196663970615f32p153e42jsn6fd048b6a909"
	}
    })
    .then(response => {
        console.log('Holaaaa');
	    console.log(response);
    })
    .catch(err => {
	console.error(err);
    });
		}
		catch(err) {
			console.log(err);
		}
	});


</script>

<main>
	<div class="container-fluid">
		
		<div class="col">
			
			<div class="col-4">
				<img class="img-responsive" src={image} alt="Foto de tu axie">
				<ul class="list-group">
					{#each parts as part}
						<li class="list-group-item"> {part.id} </li>
					{/each} 
				</ul>
			</div>
		</div>
		
	
	</div>
</main>
