<script>
  let radius = 0;
  let volume = 0;

  let radiusUnit = "";

  let units = [
    { id: "not_selected", text: "Seçiniz." },
    { id: "yard", text: "Yard" },
    { id: "feet", text: "Fit" },
    { id: "meter", text: "Metre" },
    { id: "centimeter", text: "Santimetre" }
  ];

  function changeSelectElement() {
    if (radiusUnit.id != "not_selected" && radiusUnit.id != undefined) 
    {
      volume = ((4/3) * Math.PI * Math.pow(radius, 3)).toFixed(2);
    }
  }
</script>

<main>
  <div class="container text-center">
    <div class="row">
      <div class="col-12">
        <img src="images/sphere-volume-formula.png" alt="sphere" width="50%" />
      </div>
      <div class="col-6">
        <div class="input-group mb-3">
          <div class="input-group-prepend">
            <span
              class="input-group-text bg-primary text-white"
              id="radius-label">
              Yarıçap
            </span>
          </div>
          <input
            type="number"
            class="form-control"
            aria-describedby="radius-label"
            bind:value={radius}
            on:change={changeSelectElement} />
        </div>
      </div>
      <div class="col-6">
        <div class="input-group mb-3">
          <div class="input-group-prepend">
            <span
              class="input-group-text bg-primary text-white"
              id="radius-label">
              Birim
            </span>
          </div>
          <select
            type="number"
            class="form-control"
            aria-describedby="edge-label"
            bind:value={radiusUnit}
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
              {radiusUnit.text == undefined ? 'br' : radiusUnit.text}
              <sup>3</sup>
            </span>
          </h3>
        </div>
      </div>
    </div>
  </div>
</main>
