<script>
  export let grid;
  import Specs from "./Specs.svelte";
  import Preview from "./Preview.svelte";
</script>

<style>
  div {
    flex: 0;
    display: flex;
    flex-direction: column;
    padding: 40px 40px 20px;
    border-bottom: 1px solid rgba(213, 218, 221, 0.5);
  }
</style>

<div>
  <Specs {grid} />
  <Preview {grid} />
</div>
