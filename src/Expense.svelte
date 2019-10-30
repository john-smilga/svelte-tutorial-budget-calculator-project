<script>
  import { slide } from "svelte/transition";
  export let id;
  export let name = "";
  export let amount = 0;
  export let index;
  // export let removeExpense;
  let displayAmount = false;
  function toggleAmount() {
    displayAmount = !displayAmount;
  }
  import { getContext } from "svelte";
  const removeExpense = getContext("remove");
  const setModifiedExpense = getContext("modify");
</script>

<!-- <article class="single-expense" transition:scale={{ duration: 2000 }}> -->
<!-- <article class="single-expense" transition:blur={{ duration: 2000 }}> -->
<!-- <article class="single-expense" transition:fade={{ duration: 2000 }}> -->
<!-- <article class="single-expense" transition:fade={{ duration: 2000 }}> -->
<!-- <article class="single-expense" transition:slide={{ duration: 2000 }}> -->
<!-- <article class="single-expense" transition:fly={{ duration: 2000 }}> -->
<article class="single-expense">
  <div class="expense-info">
    <h2>
      {name}
      <button class="amount-btn" on:click={toggleAmount}>
        <i class="fas fa-caret-down" />
      </button>
    </h2>
    {#if displayAmount}
      <h4 transition:slide>amount : ${amount}</h4>
    {/if}
  </div>
  <div class="expense-buttons">
    <button
      class="expense-btn edit-btn"
      on:click={() => setModifiedExpense(id)}>
      <i class="fas fa-pen" />
    </button>
    <button class="expense-btn delete-btn" on:click={() => removeExpense(id)}>
      <i class="fas fa-trash" />
    </button>
  </div>
</article>
