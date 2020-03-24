<script>
  export let grid;
</script>

<style>
  section {
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
    margin-bottom: 20px;
  }
  div {
    margin-right: 40px;
  }

  h3 {
    color: var(--color-gray-mid);
    font-size: 14px;
    font-weight: 700;
    line-height: 1;
    margin-bottom: 8px;
  }

  h2 {
    color: var(--color-gray-dark);
    font-size: 32px;
    font-weight: 700;
    line-height: 1;
  }
</style>

<section>
  <div>
    <h3>Column width:</h3>
    <h2>{grid.column}</h2>
  </div>
  <div>
    <h3>Gutter width:</h3>
    <h2>{grid.gutter}</h2>
  </div>
</section>
