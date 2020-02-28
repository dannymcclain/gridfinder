<script>
  import { onMount } from "svelte";
  import { createEventDispatcher } from "svelte";

  let totalWidth = 1200;
  let columns = 12;
  let minGutter = 20;
  let marginRatio = 0;

  const dispatch = createEventDispatcher();

  function sendGrids() {
    dispatch("calculate", {
      data: {
        totalWidth: `${totalWidth}`,
        columns: `${columns}`,
        minGutter: `${minGutter}`,
        marginRatio: `${marginRatio}`
      }
    });
  }

  onMount(() => {
    document.addEventListener("keydown", event => {
      if (event.code === "Enter") {
        sendGrids();
      }
    });
    sendGrids();
  });
</script>

<style>
  .inputs {
    margin-bottom: 40px;
  }
  label {
    font-weight: 700;
    font-size: 0.8rem;
    margin-bottom: 8px;
  }
  input {
    border: 2px solid #ccc;
    transition: border-color 200ms cubic-bezier(0.4, 0, 0, 1);
    padding: 16px;
    margin-bottom: 20px;
    border-radius: 8px;
  }
  input:focus {
    outline: none;
    border: 2px solid #90f;
  }
</style>

<section class="inputs">
  <label>Total Width</label>
  <input type="number" bind:value={totalWidth} />

  <label>Number of Columns</label>
  <input type="number" bind:value={columns} />

  <label>Minimum Gutter</label>
  <input type="number" bind:value={minGutter} />

  <button on:click={sendGrids}>Calculate</button>
</section>
