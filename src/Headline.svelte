<script>
  export let howMany;
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  function openModal() {
    dispatch("open", {
      data: {
        isOpen: true
      }
    });
  }
</script>

<style>
  header {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    max-width: 860px;
    margin-bottom: 40px;
  }
  h1 {
    font-size: 32px;
    font-weight: 800;
    line-height: 38px;
  }
  h1 span {
    margin-right: 4px;
    color: var(--color-accent);
  }
  .info {
    font-size: 12px;
    font-weight: 800;
    letter-spacing: -0.02em;
    line-height: 14px;
    color: var(--color-accent);
    display: flex;
    flex-direction: row;
    justify-content: flex-start;
    align-items: center;
    flex-wrap: nowrap;
  }
  .info:hover {
    cursor: pointer;
    color: var(--color-accent-dark);
  }
  .info img {
    margin-right: 4px;
  }
</style>

<header>
  <h1>
    <span class="accent">{howMany}</span>
    Pixel Grids
  </h1>
  <div class="info" on:click={openModal}>
    <img src="./images/icon-info.svg" alt="info icon" />
    <p>Info</p>
  </div>
</header>
