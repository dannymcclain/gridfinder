<script>
  import Info from "./Components/Info.svelte";
  import Header from "./Components/Header.svelte";
  import Form from "./Components/Form/Form.svelte";
  import Preview from "./Components/Preview/Preview.svelte";
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
  @import url("https://fonts.googleapis.com/css2?family=Inter:wght@400;800&display=swap");

  :global(:root) {
    --color-accent: #45e560;
    --color-accent-dark: #0099e5;
    --color-gray-ultralight: #f7fbfc;
    --color-gray-light: #d5dadd;
    --color-gray-mid: #878e92;
    --color-gray-dark: #0f2e3d;
    --color-white: #fff;
    --drop-shadow: 0px 2px 4px rgba(199, 206, 209, 0.4);
  }
  :global(body) {
    font-family: "Inter", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
      Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
    font-weight: 400;
    color: #000;
    background: #45e560;
  }

  main {
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    max-width: 1280px;
    margin: 0 auto;
  }
</style>

<Info {isOpen} on:close={closeInfo} />
<main>
  <Header howMany={gridLayouts.length} on:open={openModal} />
  <Form on:calculate={calculateValues} />
  <Preview grids={gridLayouts} />
</main>
