<script>
  import SectionTitle from "./SectionTitle.svelte";
  import Expense from "./Expense.svelte";
  import { scale, blur, fade, slide, fly } from "svelte/transition";
  import { flip } from "svelte/animate";
  export let expenses = [];
</script>

<section>
  <SectionTitle title="expenses list" />
  {#each expenses as expense, index (expense.id)}
    <div animate:flip transition:fly={{ delay: index * 700, x: 200 }}>
      <Expense {...expense} {index} />
    </div>
  {:else}
    <h3>No Expenses Added to the List!</h3>
  {/each}
</section>
