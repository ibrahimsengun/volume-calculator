<script>
  let edge = 0;
  let volume = 0;

  let edgeUnit = "";

  let units = [
    { id: "not_selected", text: "Seçiniz." },
    { id: "yard", text: "Yard" },
    { id: "feet", text: "Fit" },
    { id: "meter", text: "Metre" },
    { id: "centimeter", text: "Santimetre" }
  ];

  function changeSelectElement() {
    if (edgeUnit.id != "not_selected" && edgeUnit.id != undefined) 
    {
      volume = Math.pow(edge, 3);
    }
  }
</script>

<main>
  <div class="container text-center">
    <div class="row">
      <div class="col-12">
        <img src="images/volume-cube.jpg" alt="cube" width="50%" />
      </div>
      <div class="col-6">
        <div class="input-group mb-3">
          <div class="input-group-prepend">
            <span
              class="input-group-text bg-primary text-white"
              id="edge-label">
              Kenar
            </span>
          </div>
          <input
            type="number"
            class="form-control"
            aria-describedby="edge-label"
            bind:value={edge}
            on:change={changeSelectElement} />
        </div>
      </div>
      <div class="col-6">
        <div class="input-group mb-3">
          <div class="input-group-prepend">
            <span
              class="input-group-text bg-primary text-white"
              id="edge-label">
              Birim
            </span>
          </div>
          <select
            type="number"
            class="form-control"
            aria-describedby="edge-label"
            bind:value={edgeUnit}
            on:change={changeSelectElement}>
            {#each units as unit}
              <option value={unit}>{unit.text}</option>
            {/each}
            </select>
        </div>
      </div>
      <div class="col-12 mt-3">
        <div class="alert alert-primary">
          <h3>
            <span class="badge">Hacim :</span>
            {volume}
            <span class="badge">
              {edgeUnit.text == undefined ? 'br' : edgeUnit.text}
              <sup>3</sup>
            </span>
          </h3>
        </div>
      </div>
    </div>
  </div>
</main>
