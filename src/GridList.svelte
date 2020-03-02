<script>
  export let grids;
</script>

<style>
  .grid-previews-container {
    flex: 1;
    display: flex;
    flex-direction: column;
    background: var(--color-white);
    border: 1px solid var(--gray-color-light);
    border-radius: 4px;
  }
  .layout {
    display: flex;
    flex-direction: column;
    padding: 40px;
    border-bottom: 1px solid var(--gray-color-light);
    overflow-x: scroll;
  }
  .grid-preview {
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
  }
  .specs {
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
    margin-bottom: 20px;
  }

  .specs p {
    margin-right: 20px;
  }

  .specs p .value-text {
    font-weight: bold;
  }
  .margin {
    flex: none;
    height: 40px;
    background: var(--color-white);
    /* opacity: 0.2; */
  }

  .column {
    flex: none;
    height: 40px;
    background: var(--accent-color);
    border-radius: 2px;
  }

  .gutter {
    flex: none;
    height: 40px;
    background: var(--color-white);
    /* opacity: 0.15; */
  }
</style>

<section class="grid-previews-container">
  {#each grids as grid, i}
    <div class="layout" key={'Layout ' + i}>
      <div class="specs">
        <p>
          Column:
          <span class="value-text">{grid.column}</span>
        </p>
        <p>
          Gutter:
          <span class="value-text">{grid.gutter}</span>
        </p>
        <p>
          Margin:
          <span class="value-text">{grid.margin}</span>
        </p>
      </div>
      <div class="grid-preview">
        <div class="margin" style="width: {grid.margin}px" />
        {#each Array(grid.columns - 1) as columnPreview, i}
          <div class="column" style="width: {grid.column}px" />
          <div class="gutter" style="width: {grid.gutter}px" />
        {/each}
        <div class="column" style="width: {grid.column}px;" />
        <div class="margin" style="width: {grid.margin}px;" />
      </div>

    </div>
  {:else}
    <p>No grids. Bummer.</p>
  {/each}
</section>
