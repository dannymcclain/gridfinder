<script>
  export let grids;
</script>

<style>
  .grid-previews-container {
    flex: 1;
    display: flex;
    flex-direction: column;
    border: 1px solid var(--gray-color-light);
    border-radius: 4px;
    background: var(--color-white);
    box-shadow: var(--drop-shadow);
    max-width: 860px;
    position: relative;
    margin-bottom: 80px;
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
    border-bottom: 1px solid var(--gray-color-light);
  }
  .grid-preview {
    flex: 0;
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
    overflow-x: scroll;
    padding-bottom: 20px;
  }
  .specs {
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
    margin-bottom: 20px;
  }

  .specs p {
    color: var(--gray-color-mid);
    font-size: 12px;
    font-weight: 800;
    letter-spacing: -0.02em;
    line-height: 14px;
    margin-right: 12px;
  }

  .specs p .value-text {
    color: var(--gray-color-dark);
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
  .no-grids {
    padding: 40px;
  }
</style>

<section class="grid-previews-container">
  {#each grids as grid, i}
    <div class="layout" key={'Layout ' + i}>
      <div class="specs">
        <p>
          Column width:
          <span class="value-text">{grid.column}</span>
        </p>
        <p>
          Gutter width:
          <span class="value-text">{grid.gutter}</span>
        </p>
        <!-- <p>
          Margin:
          <span class="value-text">{grid.margin}</span>
        </p> -->
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
    <p class="no-grids">🤷‍♂️ No grids. Bummer.</p>
  {/each}
</section>
