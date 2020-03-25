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
    align-items: flex-start;
    padding: 20px;
  }
  h1 {
    font-size: 32px;
    line-height: 38px;
    font-weight: 800;
    color: #000000;
  }
  h1 span {
    color: #fff;
    display: block;
  }
  .info {
    height: 40px;
    width: 40px;
    border-radius: 50%;
    background: #000000;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    flex-wrap: nowrap;
  }
  .info:hover {
    cursor: pointer;
  }
  .info img {
    margin-bottom: 2px;
  }
  @media (min-width: 520px) {
    header {
      padding: 40px 40px 20px;
    }
    h1 {
      font-size: 48px;
      line-height: 56px;
      letter-spacing: -0.02em;
    }
  }

  @media (min-width: 680px) {
    header {
      padding: 80px 40px 40px;
    }
    h1 {
      font-size: 64px;
      line-height: 77px;
      letter-spacing: -0.02em;
    }
  }
  @media (min-width: 960px) {
    header {
      padding: 80px 80px 40px;
    }
  }
</style>

<header>
  <h1>
    Grid Finder
    <span class="accent">found {howMany} grids.</span>
  </h1>
  <div class="info" on:click={openModal}>
    <img src="./images/icon-info.svg" alt="info icon" />
  </div>
</header>
