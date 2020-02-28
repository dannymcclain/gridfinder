<script>
  export let grids = [];
</script>

<style>
  .grid-previews-container {
    flex: 1;
    display: flex;
    flex-direction: column;
  }
  .grid-preview {
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
  }
  .layout {
    display: flex;
    flex-direction: column;
    margin-bottom: 40px;
  }
  .specs {
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
    margin-bottom: 12px;
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
    background: #90f;
    opacity: 0.2;
  }

  .column {
    flex: none;
    height: 40px;
    background: #90f;
  }

  .gutter {
    flex: none;
    height: 40px;
    background: #90f;
    opacity: 0.15;
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
        <div class="column" style="width: {grid.column}px" />
        <div class="margin" style={{ width: grid.margin + 'px' }} />
      </div>

    </div>
  {:else}
    <p>No grids. Bummer.</p>
  {/each}
</section>
