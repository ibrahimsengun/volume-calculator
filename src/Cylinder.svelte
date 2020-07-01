<script>
  let radius = 0;
  let height = 0;
  let volume = 0;

  let unitRadius = "";
  let unitHeight = "";
  let unitVolume = "";

  let units = [
    { id: "not_selected", text: "Seçiniz." },
    { id: "yard", text: "Yard" },
    { id: "feet", text: "Fit" },
    { id: "meter", text: "Metre" },
    { id: "centimeter", text: "Santimetre" }
  ];

  let vUnits = [
    { id: "not_selected", text: "Seçiniz." },
    { id: "liter", text: "Litre" },
    { id: "abdgal", text: "ABD Galon" },
    { id: "enggal", text: "İngiltere Galon" },
    { id: "metercub", text: "Metreküp" },
    { id: "mililiter", text: "Mililitre" }
  ];

  function changeSelectElement() {
    if (
      unitHeight.id != "not_selected" &&
      unitHeight.id != undefined &&
      (unitRadius.id != "not_selected" && unitRadius.id != undefined) &&
      (unitVolume.id != "not_selected" && unitVolume.id != undefined)
    ) {
      let r = unitConvert(radius, unitRadius.id, unitHeight.id);
      let v = (Math.PI * (r * r) * height).toFixed(2);
      volume = vUnitConvert(v, unitHeight.id, unitVolume.id).toFixed(2);
    }
  }

  function vUnitConvert(num, unit1, unit2) {
    if (unit1 == "meter") {
      if (unit2 == "metercub") {
        return num;
      } else if (unit2 == "abdgal") {
        return num * 264.172052;
      } else if (unit2 == "enggal") {
        return num * 219.97;
      } else if (unit2 == "liter") {
        return num / 0.001;
      } else if (unit2 == "mililiter") {
        return num / 0.000001;
      }
    } else if (unit1 == "centimeter") {
      if (unit2 == "metercub") {
        return num / 1000000;
      } else if (unit2 == "abdgal") {
        return num * 0.00026417;
      } else if (unit2 == "enggal") {
        return num * 0.00021997;
      } else if (unit2 == "liter") {
        return num / 1000;
      } else if (unit2 == "mililiter") {
        return num;
      }
    } else if (unit1 == "yard") {
      if (unit2 == "metercub") {
        return num / 1.308;
      } else if (unit2 == "abdgal") {
        return num * 201.97;
      } else if (unit2 == "enggal") {
        return num * 168.18;
      } else if (unit2 == "liter") {
        return num / 0.001308;
      } else if (unit2 == "mililiter") {
        return num / 0.000001308;
      }
    } else if (unit1 == "feet") {
      if (unit2 == "metercub") {
        return num / 35.315;
      } else if (unit2 == "abdgal") {
        return num * 7.4805;
      } else if (unit2 == "enggal") {
        return num * 6.2288;
      } else if (unit2 == "liter") {
        return num / 0.035315;
      } else if (unit2 == "mililiter") {
        return num / 0.000035315;
      }
    }
  }

  function unitConvert(num, unit1, unit2) {
    if (unit1 == "meter") {
      if (unit2 == "meter") {
        return num;
      } else if (unit2 == "yard") {
        return num * 1.0936;
      } else if (unit2 == "feet") {
        return num * 3.2808;
      } else if (unit2 == "centimeter") {
        return num / 0.01;
      }
    } else if (unit1 == "centimeter") {
      if (unit2 == "centimeter") {
        return num;
      } else if (unit2 == "yard") {
        return num * 0.010936;
      } else if (unit2 == "feet") {
        return num * 0.032808;
      } else if (unit2 == "meter") {
        return num / 100;
      }
    } else if (unit1 == "yard") {
      if (unit2 == "yard") {
        return num;
      } else if (unit2 == "centimeter") {
        return num / 0.010936;
      } else if (unit2 == "feet") {
        return num * 3;
      } else if (unit2 == "meter") {
        return num / 1.0936;
      }
    } else if (unit1 == "feet") {
      if (unit2 == "feet") {
        return num;
      } else if (unit2 == "centimeter") {
        return num / 0.032808;
      } else if (unit2 == "inch") {
        return num * 12;
      } else if (unit2 == "yard") {
        return num * 0.33333;
      } else if (unit2 == "meter") {
        return num / 3.2808;
      }
    }
  }

  function numberWithCommas(x) {
    return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
  }
</script>

<main>
  <div class="container text-center mt-3">
    <div class="row">
      <div class="col-12 mb-3">
        <img src="images/cylinder-volume-formula.png" alt="cylinder" />
      </div>
      <div class="col-6">
        <div class="input-group mb-3">
          <div class="input-group-prepend">
            <span
              class="input-group-text bg-primary text-white"
              id="radius-label">
              Yarıçap (r)
            </span>
          </div>
          <input
            type="number"
            class="form-control"
            aria-describedby="radius-label"
            bind:value={radius}
            on:change={changeSelectElement} />
        </div>
        <div class="input-group mb-3">
          <div class="input-group-prepend">
            <span
              class="input-group-text bg-primary text-white"
              id="radius-unit">
              Birim
            </span>
          </div>
          <select
            class="custom-select"
            aria-describedby="radius-unit"
            bind:value={unitRadius}
            on:change={changeSelectElement}>
            {#each units as unit}
              <option value={unit}>{unit.text}</option>
            {/each}
          </select>
        </div>
      </div>
      <div class="col-6">
        <div class="input-group mb-3">
          <div class="input-group-prepend">
            <span
              class="input-group-text bg-primary text-white"
              id="height-label">
              Yükseklik (h)
            </span>
          </div>
          <input
            type="number"
            class="form-control"
            aria-describedby="height-label"
            bind:value={height}
            on:change={changeSelectElement} />
        </div>
        <div class="input-group mb-3">
          <div class="input-group-prepend">
            <span
              class="input-group-text bg-primary text-white"
              id="height-unit">
              Birim
            </span>
          </div>
          <select
            class="custom-select"
            aria-describedby="height-unit"
            bind:value={unitHeight}
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
            {numberWithCommas(volume)}
            <span class="badge">
              {unitVolume.text == undefined ? 'br' : unitVolume.text}
            </span>
          </h3>
          <div class="input-group mb-3">
            <div class="input-group-prepend">
              <span
                class="input-group-text bg-primary text-white"
                id="volume-unit">
                Birim
              </span>
            </div>
            <select
              class="custom-select"
              aria-describedby="volume-unit"
              bind:value={unitVolume}
              on:change={changeSelectElement}>
              {#each vUnits as unit}
                <option value={unit}>{unit.text}</option>
              {/each}
            </select>
          </div>
        </div>
      </div>
    </div>
  </div>
</main>
