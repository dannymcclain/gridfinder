<script>
  export let value;
  export let label;
  export let src;
</script>

<style>
  div {
    display: flex;
    flex-direction: column-reverse;
  }
  label {
    font-weight: 800;
    font-size: 12px;
    line-height: 15px;
    letter-spacing: 0.01em;
    color: #000000;
    margin-bottom: 8px;
    color: var(--color-gray-dark);
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
    outline: 0;
    border: 2px solid transparent;
    border-radius: 4px;
    padding: 16px;
    font-size: 20px;
    line-height: 20px;
    color: #000000;
    /* transition: border-color 200ms linear; */
  }
  input:focus {
    border: 2px solid #000;
  }
  input[type="number"]::-webkit-inner-spin-button,
  input[type="number"]::-webkit-outer-spin-button {
    -webkit-appearance: none;
    margin: 0;
  }
  input[type="number"] {
    -moz-appearance: textfield;
  }
</style>

<div>
  <input size="1" type="number" bind:value />
  <label>
    <img {src} alt="{label} icon" />
    {label}
  </label>
</div>
