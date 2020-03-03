<script>
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
  }
  .info.is-open {
    opacity: 1;
    pointer-events: auto;
  }
  .info-overlay {
    flex-grow: 2;
    height: 100%;
    position: relative;
    background: rgba(11, 21, 47, 0.4);
    opacity: 0;
    transition: opacity 150ms linear;
  }
  .info.is-open .info-overlay {
    opacity: 1;
  }
  .info-panel {
    padding: 40px 80px 40px 40px;
    height: 100%;
    position: relative;
    background: var(--color-white);
    max-width: 480px;
    transform: translateX(200px);
    opacity: 0;
    transition: transform 200ms cubic-bezier(0.35, 0, 0, 1),
      opacity 250ms linear;
    transition-delay: 100ms;
  }
  .info.is-open .info-panel {
    transform: translateX(0);
    opacity: 1;
  }
  h2 {
    font-weight: 800;
    font-size: 32px;
    line-height: 38px;
    color: var(--gray-color-dark);
  }
  p {
    font-weight: 500;
    font-size: 16px;
    line-height: 28px;
    color: var(--gray-color-mid);
  }
</style>

<div class="info {isOpen ? 'is-open' : ''}">
  <!-- <div class="info-overlay" on:click={closeModal} /> -->
  <div class="info-panel">
    <p on:click={closeModal}>CLOSE</p>
    <h2>About</h2>
    <p>
      Pixel Grids is a simple tool to help you calculate pixel-perfect grids.
      Enter the total width of your content, the number of columns of want, and
      the minimum size you’d accept for your gutters and Pixel Grids will
      calculate every grid layout that contains only whole pixel values.
    </p>
  </div>
</div>
