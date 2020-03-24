<script>
  import { onMount } from "svelte";
  import { onDestroy } from "svelte";
  import { createEventDispatcher } from "svelte";
  import Input from "./Input.svelte";

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
    margin: 0 20px 40px;
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;
    background: rgba(255, 35, 35, 0.3);
  }
  .form {
    display: flex;
    flex-direction: column-reverse;
    background: green;
  }
  /* label {
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
    min-width: 0;
    box-sizing: border-box;
    width: 100%;
    margin: 0;
  }
  input:focus {
  } */
  button {
    margin: 0;
  }

  /* input[type="number"]::-webkit-inner-spin-button,
  input[type="number"]::-webkit-outer-spin-button {
    -webkit-appearance: none;
    margin: 0;
  } */

  @media (min-width: 680px) {
    section {
      grid-template-columns: 1fr 1fr 1fr 1fr;
      grid-gap: 20px;
    }
  }
</style>

<section>
  <div class="form">
    <!-- <input
      size="1"
      class="total-width-input"
      type="number"
      bind:value={totalWidth} />
    <label class="label">
      <img src="./images/icon-totalWidth.svg" alt="Total width icon" />
      Total Width
    </label> -->
    <Input
      bind:value={totalWidth}
      label="Total Width"
      src="./images/icon-totalWidth.svg" />
  </div>

  <div class="form">
    <input size="1" type="number" bind:value={columns} />
    <label class="label">
      <img src="./images/icon-columns.svg" alt="Total width icon" />
      Columns
    </label>
  </div>

  <div class="form">
    <input size="1" type="number" bind:value={minGutter} />
    <label class="label">
      <img src="./images/icon-minGutter.svg" alt="Total width icon" />
      Min. Gutter
    </label>
  </div>

  <div class="form">
    <button on:click={sendGrids}>Calculate</button>
  </div>
</section>
