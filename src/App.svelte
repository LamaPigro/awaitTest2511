<script>
  async function GetPowerPlant() {
    const response = await fetch("https://raw.githubusercontent.com/cristianst85/GeoNuclearData/master/data/json/denormalized/nuclear_power_plants.json") 

    if (response.ok) {
      const data = await response.json()
      return data
    } else {
      throw new Error(error)
    }
  }
</script>

{#await GetPowerPlant()}
  <div>Loading...</div>
{:then plants}
  <div class=flex>
    <div class=flex-1>
      {#each plants as plant}
        <pre> {plant.Id}. {plant.Name} </pre>
      {/each}
    </div>
    <div class=flex-2>
      <button class="btn btn-primary">Button</button>
    </div>
  </div>
  
{:catch error}
  <div class="alert alert-error shadow-lg">
    <div>
      <svg xmlns="http://www.w3.org/2000/svg" class="stroke-current flex-shrink-0 h-6 w-6" fill="none" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 14l2-2m0 0l2-2m-2 2l-2-2m2 2l2 2m7-2a9 9 0 11-18 0 9 9 0 0118 0z" /></svg>
      <span>Errore!! La fetch non è stata caricata correttamente!</span>
    </div>
  </div>
{/await}
