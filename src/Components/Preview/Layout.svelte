<script>
  export let grid;
  export let key;
</script>

<style>
  section {
    flex: 0;
    display: flex;
    flex-direction: column;
    padding: 20px;
    border-bottom: 1px solid rgba(213, 218, 221, 0.5);
  }
  .specs {
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
    margin-bottom: 20px;
  }
  .specs div {
    margin-right: 40px;
  }

  .specs h3 {
    color: var(--color-gray-mid);
    font-size: 14px;
    font-weight: 700;
    line-height: 1;
    margin-bottom: 8px;
  }

  .specs h2 {
    color: var(--color-gray-dark);
    font-size: 32px;
    font-weight: 700;
    line-height: 1;
  }

  .preview {
    flex: 0;
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
    overflow-x: hidden;
    padding-bottom: 20px;
  }

  .preview .column {
    flex: none;
    height: 8px;
    border-radius: 1px;
    background: var(--color-accent);
    opacity: 0.35;
  }
  .preview .gutter {
    flex: none;
    height: 8;
    background: var(--color-white);
  }

  @media (min-width: 680px) {
    section {
      padding: 40px 40px 20px;
    }
  }
</style>

<section {key}>
  <div class="specs">
    <div>
      <h3>Column width:</h3>
      <h2>{grid.column}</h2>
    </div>
    <div>
      <h3>Gutter width:</h3>
      <h2>{grid.gutter}</h2>
    </div>
  </div>

  <div class="preview">
    {#each Array(grid.columns - 1) as columnPreview, i}
      <div class="column" style="width: {grid.column}px" />
      <div class="gutter" style="width: {grid.gutter}px" />
    {/each}
    <div class="column" style="width: {grid.column}px;" />
  </div>
</section>
