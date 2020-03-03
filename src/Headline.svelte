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
  }
  h1 {
    font-size: 32px;
    font-weight: 800;
    margin-bottom: 40px;
    line-height: 38px;
  }
  h1 span {
    margin-right: 4px;
    color: var(--accent-color);
  }
  .info {
    padding: 20px 0 20px 20px;
  }
  .info:hover {
    cursor: pointer;
  }
</style>

<header>
  <h1>
    <span class="accent">{howMany}</span>
    Pixel Grids
  </h1>
  <img
    class="info"
    on:click={openModal}
    src="./images/icon-info.svg"
    alt="info icon" />
</header>
