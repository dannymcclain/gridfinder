<script>
  export let value;
  export let label;
  export let src;
</script>

<style>
  label {
    font-size: 14px;
    font-weight: 700;
    line-height: 1;
    margin-bottom: 8px;
    /* color: var(--color-gray-dark); */
    color: red;
    transition: color 200ms linear;
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
    justify-content: flex-start;
    align-items: center;
  }
  label img {
    margin-right: 8px;
  }
  input {
    min-width: 0;
    box-sizing: border-box;
    width: 100%;
    margin: 0;
  }

  input[type="number"]::-webkit-inner-spin-button,
  input[type="number"]::-webkit-outer-spin-button {
    -webkit-appearance: none;
    margin: 0;
  }
</style>

<input size="1" type="number" bind:value />
<label>
  <img {src} alt="{label} icon" />
  {label}
</label>
