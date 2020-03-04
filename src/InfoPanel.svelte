<script>
  import { onMount } from "svelte";
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
    background: rgba(11, 21, 47, 0.4);
    transition: opacity 150ms linear;
  }
  .info.is-open {
    opacity: 1;
    pointer-events: auto;
  }

  .info-panel {
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: flex-start;
    padding: 40px 80px 40px 40px;
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
    margin-bottom: 40px;
    display: flex;
    flex-direction: row;
    justify-content: flex-start;
    align-items: center;
    flex-wrap: nowrap;
  }
  .close img {
    margin-right: 4px;
  }
  .close p {
    font-size: 12px;
    font-weight: 800;
    letter-spacing: -0.02em;
    line-height: 14px;
    color: var(--color-accent);
  }
  .close:hover {
    cursor: pointer;
  }
  .close:hover p {
    color: var(--color-accent-dark);
  }
  h2 {
    font-weight: 800;
    font-size: 32px;
    line-height: 38px;
    color: var(--color-gray-dark);
    margin-bottom: 20px;
  }
  p {
    font-weight: 500;
    font-size: 16px;
    line-height: 28px;
    color: var(--color-gray-mid);
  }
  strong {
    font-weight: 700;
  }
  .created-by {
    margin-top: 40px;
  }
  a {
    font-size: 12px;
    font-weight: 800;
    letter-spacing: -0.02em;
    line-height: 14px;
    color: var(--color-accent);
    text-decoration: none;
  }
  a:hover {
    color: var(--color-accent-dark);
  }
</style>

<div class="info {isOpen ? 'is-open' : ''}">
  <div class="info-panel">
    <div class="close" on:click={closeModal}>
      <img src="./images/icon-close.svg" alt="close icon" />
      <p>Close</p>
    </div>
    <h2>About</h2>
    <p>
      Pixel Grids is a simple tool to help you calculate pixel-perfect grids.
      Enter the
      <strong>total width</strong>
      of your content, the
      <strong>number of columns</strong>
      you want, and the
      <strong>minimum gutter</strong>
      size you’d accept, and Pixel Grids will calculate every grid layout that
      contains only whole pixel values.
    </p>
    <a class="created-by" href="https://dannymcclain.com" target="_blank">
      ✌️ Created by Danny McClain
    </a>
  </div>
</div>
