<script>
  import { onMount } from "svelte";
  import { onDestroy } from "svelte";
  import { createEventDispatcher } from "svelte";
  export let isOpen = false;

  const dispatch = createEventDispatcher();

  function closeModal() {
    dispatch("close", {
      data: {
        isOpen: false
      }
    });
  }

  onMount(() => {
    document.addEventListener("keydown", event => {
      if (event.which === 27) {
        closeModal();
      }
    });
  });
  onDestroy(() => {
    document.removeEventListener("keydown", event);
  });
</script>

<style>
  @import url("https://fonts.googleapis.com/css?family=Roboto+Mono:500&display=swap");

  .info {
    display: flex;
    flex-direction: row;
    justify-content: flex-end;
    align-items: flex-end;
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    z-index: 11;
    pointer-events: none;
    opacity: 0;
    transition: opacity 150ms linear;
    background: rgba(69, 229, 96, 0.8);
  }
  .info.is-open {
    opacity: 1;
    pointer-events: auto;
  }

  .info-panel {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: flex-start;
    padding: 20px;
    height: 100%;
    position: relative;
    background: var(--color-white);
    max-width: 480px;
    transform: translateX(60px);
    opacity: 0;
    transition: transform 200ms cubic-bezier(0.35, 0, 0, 1),
      opacity 250ms linear;
  }
  .info.is-open .info-panel {
    transform: translateX(0);
    opacity: 1;
  }

  .close {
    height: 40px;
    width: 40px;
    border-radius: 50%;
    background: #000000;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    flex-wrap: nowrap;
    margin-bottom: 20px;
  }
  .close:hover {
    cursor: pointer;
  }
  .close-icon {
    transition: stroke 150ms linear;
  }
  .close:hover .close-icon {
      stroke: var(--color-accent);
    }

  h2 {
    font-size: 32px;
    line-height: 38px;
    font-weight: 800;
    color: var(--color-accent);
    margin-bottom: 20px;
  }
  p {
    font-weight: 400;
    font-size: 18px;
    line-height: 28px;
    color: var(--color-gray-dark);
  }
  .created-by {
    margin-top: 40px;
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
    justify-content: flex-start;
    align-items: center;
  }
  .created-by img {
    margin-right: 8px;
  }
  .created-by p {
    font-weight: 800;
    font-size: 12px;
    line-height: 15px;
  }
  .created-by a {
    color: #000;
    text-decoration: none;
    border-bottom: 2px solid var(--color-accent);
    transition: border-color 150ms linear;
  }
  .created-by a:hover {
    border-bottom: 2px solid #000;
  }
  @media (min-width: 520px) {
    .info-panel {
      padding: 40px;
    }
    .close {
      margin-bottom: 40px;
    }
    h2 {
      font-size: 48px;
      line-height: 56px;
      letter-spacing: -0.02em;
    }
  }
  @media (min-width: 680px) {
    .info-panel {
      padding: 40px 80px 40px 40px;
    }
    h2 {
      font-size: 64px;
      line-height: 77px;
      letter-spacing: -0.02em;
    }
  }
</style>

<div class="info {isOpen ? 'is-open' : ''}">
  <div class="info-panel">
    <div class="main-content">
      <div class="close" on:click={closeModal}>
        <svg width="12" height="12" viewBox="0 0 12 12" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path class="close-icon" d="M1 1L11 11M11 1L1 11" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
</svg>

      </div>
      <h2>About</h2>
      <p>
        Grid Finder is a tool to help you calculate perfect grids. Enter the
        total width of your content, the number of columns of want, and the
        minimum size you want your gutters and Grid Finder will calculate every
        grid layout that contains only whole values.
      </p>
    </div>
    <div class="created-by">
      <img src="./images/icon-createdBy.svg" alt="icon" />
      <p>
        Created by
        <a href="https://dannymcclain.com" target="_blank">Danny McClain</a>
      </p>
    </div>
  </div>
</div>
