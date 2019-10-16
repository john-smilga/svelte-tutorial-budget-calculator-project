<script>
  export let title = "Budget Calculator";
  export let showForm = () => {};
</script>

<nav class="nav">
  <div class="nav-center">
    <h1 class="nav-title">
      {title}{title.length > 20 ? ' title is too long' : ''}
    </h1>
    <button type="button" class="nav-btn" on:click={showForm}>
      <i class="far fa-plus-square" />
      add expense
    </button>
  </div>
</nav>
