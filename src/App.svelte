<script>
  import Cylinder from "./Cylinder.svelte";
  import Cube from "./Cube.svelte";
  import Sphere from "./Sphere.svelte";

  let whichShape = "";

  let shapes = [
    { id: "not_selected", text: "Seçiniz." },
    { id: "cynlider", text: "Silindir" },
    { id: "cube", text: "Küp" },
    { id: "sphere", text: "Küre" }
  ];
</script>

<main>
  <div class="container mt-3">
    <div class="row">
      <div class="col-12 text-center">
        <h1 class="mb-5">Hacim Hesaplayıcı</h1>
        <div class="input-group mb-3">
          <div class="input-group-prepend">
            <span
              class="input-group-text bg-primary text-white"
              id="shape-type">
              Şekil
            </span>
          </div>
          <select
            class="custom-select"
            aria-describedby="radius-unit"
            bind:value={whichShape}>
            {#each shapes as shape}
              <option value={shape}>{shape.text}</option>
            {/each}
          </select>
        </div>
      </div>
      <div class="col-12">
        {#if whichShape.id == "cynlider"}
          <Cylinder/>
        {:else if whichShape.id == "cube"}
          <Cube/>
        {:else if whichShape.id == "sphere"}
          <Sphere/>
        {/if}
      </div>
    </div>
  </div>

</main>
