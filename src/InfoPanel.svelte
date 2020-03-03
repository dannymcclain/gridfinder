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
    /* transition-delay: 100ms; */
  }
  .info.is-open .info-panel {
    transform: translateX(0);
    opacity: 1;
  }
  .close {
    margin-bottom: 40px;
  }
  .close:hover {
    cursor: pointer;
  }
  h2 {
    font-weight: 800;
    font-size: 32px;
    line-height: 38px;
    color: var(--gray-color-dark);
    margin-bottom: 20px;
  }
  p {
    font-weight: 500;
    font-size: 16px;
    line-height: 28px;
    color: var(--gray-color-mid);
  }
  code {
    font-family: Consolas, Menlo, monospace;
    font-size: 13px;
    padding: 4px 6px;
    font-weight: 600;
    /* color: var(--accent-color); */
    border: 1px solid var(--gray-color-light);
    background: #fafcfd;
    border-radius: 2px;
  }
  .created-by {
    margin-top: 40px;
    font-size: 14px;
  }
  a {
    color: var(--gray-color-mid);
    text-decoration: underline;
  }
  a:hover {
    color: var(--accent-color);
  }
</style>

<div class="info {isOpen ? 'is-open' : ''}">
  <div class="info-panel">
    <img
      class="close"
      on:click={closeModal}
      src="./images/icon-close.svg"
      alt="close icon" />
    <h2>About</h2>
    <p>
      Pixel Grids is a simple tool to help you calculate pixel-perfect grids.
      Enter the
      <code>total width</code>
      of your content, the
      <code>number of columns</code>
      of want, and the
      <code>minimum gutter</code>
      size you’d accept, and Pixel Grids will calculate every grid layout that
      contains only whole pixel values.
    </p>
    <p class="created-by">
      ✌️ Created by
      <a href="https://dannymcclain.com" target="_blank">Danny McClain</a>
    </p>
  </div>
</div>
