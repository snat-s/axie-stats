<script>
    let parts = ["Energy Counter",
     "Statistics",
      "Cards",
    "Damage Calculator"];
</script>

  <nav class="navbar navbar-expand-lg ">
    <div class="container-fluid">
     
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavAltMarkup" aria-controls="navbarNavAltMarkup" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarNavDropdown">
        <ul class="navbar-nav">
          {#each parts as part}
          <li class="nav-item"><a class="nav-link" href="#DamageCalculator">{part}</a></li>
        {/each}
        </ul>
      </div>
    </div>
  </nav>

<style>

</style>
