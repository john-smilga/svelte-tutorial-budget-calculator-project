<script>
  // components
  import Navbar from "./Navbar.svelte";
  import ExpenseList from "./ExpenseList.svelte";
  import Totals from "./Totals.svelte";
  import ExpenseForm from "./ExpenseForm.svelte";
  import GithubAwait from "./GithubAwait.svelte";

  // modal
  import Modal from "./Modal.svelte";
  // data
  import expenseData from "./expenses";
  //  general imports
  import { setContext, onMount, onDestroy, afterUpdate } from "svelte";
  // copy expenses
  // let expenses = [...expenseData];
  let expenses = [];
  // set editing variables
  let setName = "";
  let setAmount = null;
  let setId = null;
  $: isEditing = setId ? true : false;
  // toggle form
  let isFormOpen = false;
  function showForm() {
    isFormOpen = true;
  }
  function hideForm() {
    isFormOpen = false;
    setName = "";
    setAmount = null;
    setId = null;
  }
  // remove expense
  function removeExpense(id) {
    expenses = expenses.filter(item => item.id !== id);
  }
  setContext("remove", removeExpense);
  setContext("modify", setModifiedExpense);
  // reactive
  $: total = expenses.reduce((acc, curr) => {
    return (acc += curr.amount);
  }, 0);
  //add expense
  function addExpense({ name, amount }) {
    let expense = { id: Math.random(), name, amount };
    expenses = [expense, ...expenses];
  }
  // setModifiedExpense
  function setModifiedExpense(id) {
    let expense = expenses.find(item => item.id === id);
    setId = expense.id;
    setName = expense.name;
    setAmount = expense.amount;
    // showForm
    showForm();
  }
  // editExpense
  function editExpense({ name, amount }) {
    expenses = expenses.map(item => {
      return item.id === setId ? { ...item, name, amount } : { ...item };
    });
    setId = null;
    setAmount = null;
    setName = "";
  }
  // clear Expenses
  function clearExpenses() {
    expenses = [];
  }
  function setLocalStorage() {
    localStorage.setItem("expenses", JSON.stringify(expenses));
  }
  onMount(() => {
    expenses = localStorage.getItem("expenses")
      ? JSON.parse(localStorage.getItem("expenses"))
      : [];
  });
  afterUpdate(() => {
    setLocalStorage();
  });
  $: console.log({ setName, setAmount });
</script>

<Navbar title="Budget Calculator" {showForm} />
<main class="content">
  <!-- <GithubAwait /> -->
  {#if isFormOpen}
    <Modal>
      <ExpenseForm
        bind:name={setName}
        bind:amount={setAmount}
        {addExpense}
        {editExpense}
        {isEditing}
        {hideForm} />
    </Modal>
  {/if}
  <Totals title="total expenses" {total} />
  <ExpenseList {expenses} />
  <button
    type="button"
    class="btn btn-primary btn-block"
    on:click={clearExpenses}>
    clear expenses
  </button>
</main>
