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
    display: flex;
    flex-direction: row;
    justify-content: flex-start;
    align-items: flex-end;
  }
  .form {
    margin-right: 20px;
  }
  label {
    font-weight: 700;
    font-size: 0.8rem;
    margin-bottom: 8px;
  }
  input {
    flex: 1;
    border: 1px solid var(--gray-color-light);
    transition: border-color 200ms linear;
    padding: 16px;
    margin-bottom: 20px;
    border-radius: 4px;
    margin: 0;
    background: var(--color-white);
    box-shadow: var(--drop-shadow);
    width: 200px;
  }
  input:focus {
    outline: none;
    border: 1px solid var(--accent-color);
  }
  button {
    width: 200px;
    cursor: pointer;
    outline: none;
    border: none;
    background: var(--accent-color);
    color: #fff;
    font-weight: bold;
    padding: 0 20px;
    border-radius: 8px;
    height: 54px;
    margin: 0;
    transition: background-color 200ms linear;
  }
  button:hover {
    background: var(--accent-color-dark);
  }
</style>

<section class="inputs">
  <div class="form">
    <label>Total Width</label>
    <input type="number" bind:value={totalWidth} />
  </div>

  <div class="form">
    <label>Number of Columns</label>
    <input type="number" bind:value={columns} />
  </div>

  <div class="form">
    <label>Minimum Gutter</label>
    <input type="number" bind:value={minGutter} />
  </div>

  <button on:click={sendGrids}>Calculate</button>
</section>
