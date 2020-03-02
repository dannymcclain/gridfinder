<script>
  import Headline from "./Headline.svelte";
  import GridForm from "./GridForm.svelte";
  import GridList from "./Gridlist.svelte";
  import { onMount } from "svelte";

  let gridLayouts = [];

  function calculateValues(event) {
    let data = event.detail.data;
    findGrids(data);
  }

  function findGrids({ totalWidth, columns, minGutter, marginRatio }) {
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
</script>

<style>
  :global(*, *::after, *::before) {
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  :global(body) {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
      Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
    padding: 80px;
  }
  :global(:root) {
    --accent-color: #7568f6;
  }
  main {
    display: flex;
    flex-direction: column;
  }
</style>

<main>
  <Headline howMany={gridLayouts.length} />
  <GridForm on:calculate={calculateValues} />
  <GridList grids={gridLayouts} />
</main>
