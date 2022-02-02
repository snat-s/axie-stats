<script>
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
  //export let name;
</script>
<main>
  
</main>
