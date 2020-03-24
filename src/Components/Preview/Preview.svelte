<script>
  import Specs from "./Specs.svelte";
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

  .layout {
    flex: 0;
    display: flex;
    flex-direction: column;
    padding: 40px 40px 20px;
    border-bottom: 1px solid rgba(213, 218, 221, 0.5);
  }
  .grid-preview {
    flex: 0;
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
    overflow-x: hidden;
    padding-bottom: 20px;
  }

  .column {
    flex: none;
    height: 8px;
    border-radius: 1px;
    background: var(--color-accent);
    opacity: 0.35;
  }
  .gutter {
    flex: none;
    height: 8;
    background: var(--color-white);
  }
  .no-grids {
    padding: 40px;
  }
</style>

<section class="grid-previews-container">
  {#each grids as grid, i}
    <div class="layout" key={'Layout ' + i}>
      <Specs {grid} />

      <div class="grid-preview">
        {#each Array(grid.columns - 1) as columnPreview, i}
          <div class="column" style="width: {grid.column}px" />
          <div class="gutter" style="width: {grid.gutter}px" />
        {/each}
        <div class="column" style="width: {grid.column}px;" />
      </div>

    </div>
  {:else}
    <p class="no-grids">🤷‍♂️ No grids. Bummer.</p>
  {/each}
</section>
