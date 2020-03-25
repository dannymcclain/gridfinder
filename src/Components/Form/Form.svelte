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
    /* margin: 0 20px 40px; */
    padding: 0 20px 40px;
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;
  }
  .calculate {
    display: flex;
    flex-direction: column-reverse;
  }

  button {
    margin: 0;
    height: 56px;
    outline: none;
    border: none;
    background: #000;
    color: #fff;
    font-weight: 800;
    font-size: 16px;
    line-height: 1;
    border-radius: 4px;
    cursor: pointer;
    transition: color 150ms linear;
  }
  button:active {
    background: #000;
    color: var(--color-accent);
  }
  @media (min-width: 520px) {
    section {
      padding: 0 40px 40px;
    }
  }

  @media (min-width: 680px) {
    section {
      grid-template-columns: 1fr 1fr 1fr 1fr;
      grid-gap: 20px;
      padding: 0 40px 60px;
    }
  }
  @media (min-width: 960px) {
    section {
      padding: 0 80px 60px;
    }
  }
</style>

<section>
  <Input
    bind:value={totalWidth}
    label="Total Width"
    src="./images/icon-totalWidth.svg" />
  <Input bind:value={columns} label="Columns" src="./images/icon-columns.svg" />
  <Input
    bind:value={minGutter}
    label="Min. Gutter"
    src="./images/icon-minGutter.svg" />

  <div class="calculate">
    <button on:click={sendGrids}>Calculate</button>
  </div>
</section>
