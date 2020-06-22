<script>
  let radius = 0;
  let height = 0;
  let volume1 = 0;
  let volume2 = 0;

  let unitRadius = "";
  let unitHeight = "";
  let unitVolume1 = "";
  let unitVolume2 = "";

  let units = [
    { id: "not_selected", text: "Seçiniz." },
    { id: "mil", text: "Mil" },
    { id: "yard", text: "Yard" },
    { id: "feet", text: "Fit" },
    { id: "inch", text: "İnc" },
    { id: "kilometer", text: "Kilometre" },
    { id: "meter", text: "Metre" },
    { id: "centimeter", text: "Santimetre" }
  ];

  function changeSelectElement() {
    if (unitHeight.id != "not_selected" && unitHeight.id != undefined &&
      (unitRadius.id != "not_selected" && unitRadius.id != undefined)
    ) {
      let r = unitConvert(radius, unitRadius.id, unitHeight.id);
      volume1 = (Math.PI * (r * r) * height).toFixed(2);
      unitVolume1 = unitHeight;

      let h = unitConvert(height, unitHeight.id, unitRadius.id);
      volume2 = (Math.PI * (radius * radius) * h).toFixed(2);
      unitVolume2 = unitRadius;
    }
  }

  function unitConvert(num, unit1, unit2) {
    if (unit1 == "meter") {
      if (unit2 == "meter") {
        return num;
      } else if (unit2 == "mil") {
        return num * 0.00062137;
      } else if (unit2 == "yard") {
        return num * 1.0936;
      } else if (unit2 == "feet") {
        return num * 3.2808;
      } else if (unit2 == "inch") {
        return num * 39.37;
      } else if (unit2 == "kilometer") {
        return num / 1000;
      } else if (unit2 == "centimeter") {
        return num / 0.01;
      }
    } else if (unit1 == "kilometer") {
      if (unit2 == "kilometer") {
        return num;
      } else if (unit2 == "mil") {
        return num * 0.62137;
      } else if (unit2 == "yard") {
        return num * 1093.6;
      } else if (unit2 == "feet") {
        return num * 3280.8;
      } else if (unit2 == "inch") {
        return num * 39370;
      } else if (unit2 == "meter") {
        return num * 1000;
      } else if (unit2 == "centimeter") {
        return num * 100000;
      }
    } else if (unit1 == "centimeter") {
      if (unit2 == "centimeter") {
        return num;
      } else if (unit2 == "mil") {
        return num * 0.0000062137;
      } else if (unit2 == "yard") {
        return num * 0.010936;
      } else if (unit2 == "feet") {
        return num * 0.032808;
      } else if (unit2 == "inch") {
        return num * 0.3937;
      } else if (unit2 == "meter") {
        return num / 100;
      } else if (unit2 == "kilometer") {
        return num / 100000;
      }
    } else if (unit1 == "mil") {
      if (unit2 == "mil") {
        return num;
      } else if (unit2 == "centimeter") {
        return num / 0.0000062137;
      } else if (unit2 == "yard") {
        return num * 1760;
      } else if (unit2 == "feet") {
        return num * 5280;
      } else if (unit2 == "inch") {
        return num * 63360;
      } else if (unit2 == "meter") {
        return num / 0.00062137;
      } else if (unit2 == "kilometer") {
        return num / 0.62137;
      }
    } else if (unit1 == "yard") {
      if (unit2 == "yard") {
        return num;
      } else if (unit2 == "centimeter") {
        return num / 0.010936;
      } else if (unit2 == "mil") {
        return num * 0.00056818;
      } else if (unit2 == "feet") {
        return num * 3;
      } else if (unit2 == "inch") {
        return num * 36;
      } else if (unit2 == "meter") {
        return num / 1.0936;
      } else if (unit2 == "kilometer") {
        return num / 1093.6;
      }
    } else if (unit1 == "inch") {
      if (unit2 == "inch") {
        return num;
      } else if (unit2 == "centimeter") {
        return num / 0.3937;
      } else if (unit2 == "mil") {
        return num * 0.000015783;
      } else if (unit2 == "feet") {
        return num * 0.083333;
      } else if (unit2 == "yard") {
        return num * 0.027778;
      } else if (unit2 == "meter") {
        return num / 39.37;
      } else if (unit2 == "kilometer") {
        return num / 39370;
      }
    } else if (unit1 == "feet") {
      if (unit2 == "feet") {
        return num;
      } else if (unit2 == "centimeter") {
        return num / 0.032808;
      } else if (unit2 == "mil") {
        return num * 0.00018939;
      } else if (unit2 == "inch") {
        return num * 12;
      } else if (unit2 == "yard") {
        return num * 0.33333;
      } else if (unit2 == "meter") {
        return num / 3.2808;
      } else if (unit2 == "kilometer") {
        return num / 3280.8;
      }
    }
  }

  function numberWithCommas(x) {
    return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
  }
</script>

<main>
  <div class="container text-center">
    <div class="row">
      <div class="col-12 mb-3">
        <h1 class="mb-3">Silindir Hacim Hesaplayıcı</h1>
        <img src="images/cylinder-volume-formula.png" alt="cylinder" />
      </div>
      <div class="col-6">
        <div class="input-group mb-3">
          <div class="input-group-prepend">
            <span class="input-group-text" id="radius-label">Yarıçap (r)</span>
          </div>
          <input
            type="number"
            class="form-control mr-3"
            aria-describedby="radius-label"
            bind:value={radius}
            on:change={changeSelectElement} />

          <div class="input-group-prepend">
            <span class="input-group-text" id="radius-unit">Birim</span>
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
            <span class="input-group-text" id="height-label">
              Yükseklik (h)
            </span>
          </div>
          <input
            type="number"
            class="form-control mr-3"
            aria-describedby="height-label"
            bind:value={height}
            on:change={changeSelectElement} />

          <div class="input-group-prepend">
            <span class="input-group-text" id="height-unit">Birim</span>
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
        <div class="card">
          <div class="card-body">
            <h3>
              Hacim 1: {numberWithCommas(volume1)} {unitVolume1.text == undefined ? 'br' : unitVolume1.text}
              <sup>3</sup>
            </h3>
          </div>
        </div>

        <div class="card">
          <div class="card-body">
            <h3>
              Hacim 2: {numberWithCommas(volume2)} {unitVolume2.text == undefined ? 'br' : unitVolume2.text}
              <sup>3</sup>
            </h3>
          </div>
        </div>

      </div>
    </div>
  </div>
</main>
