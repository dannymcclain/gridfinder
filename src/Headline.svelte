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
    color: var(--accent-color);
  }
  .info {
    padding: 12px;
  }
  .info:hover {
    cursor: pointer;
  }
  .info:hover .outer {
    stroke: #8D95A5;
  }
</style>

<header>
  <h1>
    <span class="accent">{howMany}</span>
    Pixel Grids
  </h1>
  <!-- <img
    class="info"
    on:click={openModal}
    src="./images/icon-info.svg"
    alt="info icon" /> -->
    <svg class="info"
    on:click={openModal} width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
<path d="M12 12V16" stroke="#8D95A5" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
<circle class="outer" cx="12" cy="12" r="10" stroke="#D5DDE2" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
<circle cx="12" cy="8" r="1" fill="#8D95A5"/>
</svg>

</header>
