<script>
  // import Specs from "./Specs.svelte";
  import Layout from "./Layout.svelte";
  export let grids;
</script>

<style>
  .grid-previews-container {
    margin: 0 20px 80px;
    display: flex;
    flex-direction: column;
    border-radius: 4px;
    background: var(--color-white);
    box-shadow: var(--drop-shadow);
    max-width: 860px;
    position: relative;
  }
  .grid-previews-container:after {
    content: "";
    position: absolute;
    z-index: 1;
    bottom: 0;
    left: 0;
    pointer-events: none;
    background-image: linear-gradient(
      to right,
      rgba(255, 255, 255, 0) 80%,
      rgba(255, 255, 255, 1) 95%
    );
    height: 100%;
    width: 100%;
  }

  .no-grids {
    padding: 40px;
  }
</style>

<section class="grid-previews-container">
  {#each grids as grid, i}
    <Layout {grid} key={'Layout ' + i} />
  {:else}
    <p class="no-grids">🤷‍♂️ No grids. Bummer.</p>
  {/each}
</section>
