<script>
  // import Specs from "./Specs.svelte";
  import Layout from "./Layout.svelte";
  export let grids;
</script>

<style>
  .grid-previews {
    margin: 0 20px 40px;
    display: flex;
    flex-direction: column;
    border-radius: 4px;
    background: #fff;
    position: relative;
  }
  .grid-previews:after {
    border-radius: 4px;
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

  @media (min-width: 520px) {
    .grid-previews {
      margin: 0 40px 40px;
    }
  }

  @media (min-width: 680px) {
    .grid-previews {
      margin: 0 40px 80px;
    }
  }
  @media (min-width: 960px) {
    .grid-previews {
      margin: 0 80px 80px;
    }
  }
</style>

<section class="grid-previews">
  {#each grids as grid, i}
    <Layout {grid} key={'Layout ' + i} />
  {:else}
    <p class="no-grids">🤷‍♂️ No grids. Bummer.</p>
  {/each}
</section>
