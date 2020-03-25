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
  .info-icon {
    transition: fill 150ms linear;
  }
  .info:hover {
    cursor: pointer;
  }
  .info:hover .info-icon {
    fill: #fff;
  }
  .info svg {
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
    <svg width="9" height="15" viewBox="0 0 9 15" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path class="info-icon" fill-rule="evenodd" clip-rule="evenodd" d="M4.51816 2.56003C3.75326 2.30507 2.90996 2.50414 2.33984 3.07426L1.70711 3.70699C1.31658 4.09752 0.683417 4.09752 0.292893 3.70699C-0.0976311 3.31647 -0.0976311 2.6833 0.292893 2.29278L0.925624 1.66005C2.03141 0.554263 3.66705 0.168142 5.15061 0.662664L5.56042 0.799267C8.89867 1.91202 9.22511 6.50537 6.07778 8.07903C5.41724 8.4093 5 9.08441 5 9.82291V9.99989C5 10.5522 4.55228 10.9999 4 10.9999C3.44772 10.9999 3 10.5522 3 9.99989V9.82291C3 8.32687 3.84525 6.95923 5.18335 6.29018C6.73698 5.51336 6.57584 3.24593 4.92796 2.69663L4.51816 2.56003Z" fill="#45E560"/>
      <path class="info-icon" d="M5 13.9999C5 14.5522 4.55228 14.9999 4 14.9999C3.44772 14.9999 3 14.5522 3 13.9999C3 13.4476 3.44772 12.9999 4 12.9999C4.55228 12.9999 5 13.4476 5 13.9999Z" fill="#45E560"/>
    </svg>

  </div>
</header>
