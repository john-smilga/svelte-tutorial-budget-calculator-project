<script>
  import SectionTitle from "./SectionTitle.svelte";
  import Expense from "./Expense.svelte";
  export let expenses = [];
</script>

<section>
  <SectionTitle title="expenses list" />
  <ul>
    {#each expenses as expense}
      <Expense {...expense} />
    {:else}
      <h3>No Expenses Added to the List!</h3>
    {/each}
  </ul>
</section>
