<script>
  let radius = 0;
  let height = 0;

  function numberWithCommas(x) {
    return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, " ");
}
</script>

<style>
  main {
    font-family: "Lucida Sans", "Lucida Sans Regular", "Lucida Grande",
      "Lucida Sans Unicode", Geneva, Verdana, sans-serif;
  }

  h1 {
    color: #eb5f5f;
  }

  #volume {
    font-size: 3vw;
  }
</style>

<main>
  <div class="container text-center">
    <div class="row">
      <div class="col-12 mb-3">
        <h1>Silindir Hacim Hesaplayıcı</h1>
      </div>
      <div class="col-2" />
      <div class="col-4">
        <div class="input-group mb-3">
          <div class="input-group-prepend">
            <span class="input-group-text" id="radius-label">Yarıçap</span>
          </div>
          <input
            type="number"
            class="form-control"
            aria-describedby="radius-label"
            bind:value={radius} />
        </div>
      </div>
      <div class="col-4">
        <div class="input-group mb-3">
          <div class="input-group-prepend">
            <span class="input-group-text" id="height-label">Yükseklik</span>
          </div>
          <input
            type="number"
            class="form-control"
            aria-describedby="height-label"
            bind:value={height} />
        </div>
      </div>
      <div class="col-2" />
      <div class="col-12  mt-3">
        <p id="volume">
          Hacim: {numberWithCommas((Math.PI * (radius * radius) * height).toFixed(3))}
        </p>
      </div>
    </div>
  </div>
</main>
