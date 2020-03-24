<script>
  export let grid;
</script>

<style>
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
</style>

<div class="grid-preview">
  {#each Array(grid.columns - 1) as columnPreview, i}
    <div class="column" style="width: {grid.column}px" />
    <div class="gutter" style="width: {grid.gutter}px" />
  {/each}
  <div class="column" style="width: {grid.column}px;" />
</div>
