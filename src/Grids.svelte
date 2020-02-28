<script>
  import { onMount } from "svelte";

  onMount(() => {
    document.addEventListener("keydown", event => {
      if (event.code === "Enter") {
        findGrids();
      }
    });
  });

  // create empty gridLayouts array
  let gridLayouts = [];

  // set default values
  let totalWidth = 1200;
  let columns = 12;
  let minGutter = 8;
  let marginRatio = 0;
  let columnLength = new Array(columns - 1);

  function findGrids() {
    columnLength = new Array(columns - 1);
    gridLayouts = [];
    const getWidth = gutter => {
      return totalWidth - 2 * marginRatio * gutter;
    };
    const getColumnWidth = gutter => {
      return (getWidth(gutter) - (columns - 1) * gutter) / columns;
    };
    let gutter = parseInt(minGutter);
    let columnWidth = getColumnWidth(gutter);
    let margin = marginRatio * gutter;
    while (gutter < columnWidth) {
      columnWidth = getColumnWidth(gutter);
      margin = marginRatio * gutter;
      if (columnWidth % 1 === 0) {
        const grid = {
          column: columnWidth,
          gutter: gutter,
          margin: margin,
          columns: columns
        };
        gridLayouts.push(grid);
        gridLayouts = gridLayouts;
      }
      gutter++;
    }
  }
  findGrids();
</script>

<style>
  *,
  *::after,
  *::before {
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    margin: 0;
    padding: 0;
    box-sizing: border-box;
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
    margin-bottom: 20px;
  }

  .specs p {
    margin-right: 20px;
  }

  .specs p .value-text {
    font-weight: bold;
  }

  .grid-preview {
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
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
  .accent {
    color: #90f;
  }
  main {
    padding: 80px;
  }
  h1 {
    font-weight: 900;
    margin-bottom: 40px;
    font-size: 40px;
  }
  h1 span {
    /* font-weight: 700; */
    margin-right: 4px;
  }
  .inputs {
    margin-bottom: 40px;
  }
</style>

<main>

  <h1>
    <span class="accent">{gridLayouts.length}</span>
    Pixel Grids
  </h1>
  <section class="inputs">
    <input type="number" bind:value={totalWidth} />
    <input type="number" bind:value={columns} />
    <input type="number" bind:value={minGutter} />
    <button on:click={findGrids}>Calculate</button>
  </section>
  {#each gridLayouts as grid, i}
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
        <!-- <p>There are {columns} columns.</p> -->
        {#each columnLength as columnPreview, i}
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
</main>
