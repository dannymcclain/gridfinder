<script>
  import { onMount } from "svelte";
  import { onDestroy } from "svelte";
  import { createEventDispatcher } from "svelte";

  let totalWidth = 1200;
  let columns = 12;
  let minGutter = 8;
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
  onDestroy(() => {
    document.removeEventListener("keydown", event);
  });
</script>

<style>
  section {
    margin-bottom: 40px;
    padding: 0 20px;
    /* display: grid;
    grid-template-columns: repeat(2, 20px [col-start]); */
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    background: rgba(255, 35, 35, 0.3);
  }
  .form {
    flex: auto;
    /* max-width: 200px; */
    margin-right: 0;
    display: flex;
    flex-direction: column-reverse;
    background: green;
  }
  .form:nth-child(odd) {
    margin-right: 20px;
  }
  label {
    font-size: 14px;
    font-weight: 700;
    line-height: 1;
    margin-bottom: 8px;
    color: var(--color-gray-dark);
    transition: color 200ms linear;
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
    justify-content: flex-start;
    align-items: center;
  }
  label img {
    margin-right: 8px;
  }
  input {
    flex: 1;
    min-width: 1px;
    padding: 16px;
    font-family: "Source Code Pro", monospace;
    font-weight: 500;
    font-size: 18px;
    line-height: 1;
    border: 1px solid var(--color-white);
    color: var(--color-gray-dark);
    transition: border-color 200ms linear;
    height: 60px;
    border-radius: 4px;
    margin: 0;
    background: var(--color-white);
    box-shadow: var(--drop-shadow);
  }
  input:focus {
    outline: none;
    border: 1px solid var(--color-accent);
  }
  button {
    flex: 1;
    height: 60px;
    background: var(--color-accent);
    border: none;
    border-radius: 8px;
    color: #fff;
    cursor: pointer;
    font-size: 16px;
    font-weight: 700;
    line-height: 1;
    margin: 0;
    outline: none;
    text-align: center;
    transition: background-color 200ms linear;
  }
  button:hover {
    background: var(--color-accent-dark);
  }

  input[type="number"]::-webkit-inner-spin-button,
  input[type="number"]::-webkit-outer-spin-button {
    -webkit-appearance: none;
    margin: 0;
  }
</style>

<section>
  <div class="form">
    <input class="total-width-input" type="number" bind:value={totalWidth} />
    <label class="label">
      <img src="./images/icon-totalWidth.svg" alt="Total width icon" />
      Total Width
    </label>
  </div>

  <div class="form">
    <input type="number" bind:value={columns} />
    <label class="label">
      <img src="./images/icon-columns.svg" alt="Total width icon" />
      Number of Columns
    </label>
  </div>

  <div class="form">
    <input type="number" bind:value={minGutter} />
    <label class="label">
      <img src="./images/icon-minGutter.svg" alt="Total width icon" />
      Minimum Gutter
    </label>
  </div>

  <div class="form">
    <button on:click={sendGrids}>Calculate</button>
  </div>
</section>
