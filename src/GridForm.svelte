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
    display: flex;
    flex-direction: column-reverse;
  }
  label {
    font-size: 12px;
    font-weight: 800;
    letter-spacing: -0.02em;
    line-height: 14px;
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
    border: 1px solid var(--color-white);
    color: var(--color-gray-dark);
    flex: 1;
    transition: border-color 200ms linear;
    padding: 16px;
    margin-bottom: 20px;
    border-radius: 4px;
    margin: 0;
    background: var(--color-white);
    box-shadow: var(--drop-shadow);
    width: 200px;
    font-weight: 500;
    font-size: 16px;
    line-height: 19px;
  }
  input:focus {
    outline: none;
    border: 1px solid var(--color-accent);
  }
  button {
    background: var(--color-accent);
    border: none;
    border-radius: 8px;
    color: #fff;
    cursor: pointer;
    font-size: 16px;
    font-weight: 800;
    height: 54px;
    line-height: 19px;
    letter-spacing: -0.02em;
    margin: 0;
    outline: none;
    text-align: center;
    transition: background-color 200ms linear;
    width: 200px;
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

<section class="inputs">
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

  <button on:click={sendGrids}>Calculate</button>
</section>
