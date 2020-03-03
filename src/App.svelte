<script>
  import InfoPanel from "./InfoPanel.svelte";
  import Headline from "./Headline.svelte";
  import GridForm from "./GridForm.svelte";
  import GridList from "./Gridlist.svelte";
  import { onMount } from "svelte";

  let gridLayouts = [];
  let isOpen = false;
  function openModal() {
    isOpen = true;
  }
  function closeInfo() {
    isOpen = false;
  }
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
  :global(:root) {
    --accent-color: #6d50e2;
    --accent-color-dark: #4b31af;
    --gray-color-light: #d5dde2;
    --gray-color-mid: #8d95a5;
    --gray-color-dark: #0b152f;
    --color-white: #fff;
    --drop-shadow: 0px 2px 4px rgba(213, 221, 226, 0.6);
  }
  :global(body) {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
      Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
    padding: 80px;
    color: var(--gray-color-dark);
    background: #fafcfd;
  }

  main {
    display: flex;
    flex-direction: column;
    max-width: 860px;
    margin: 0 auto;
  }
</style>

<InfoPanel {isOpen} on:close={closeInfo} />
<main>
  <Headline howMany={gridLayouts.length} on:open={openModal} />
  <GridForm on:calculate={calculateValues} />
  <GridList grids={gridLayouts} />
</main>
