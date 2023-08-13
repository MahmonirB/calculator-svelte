<script>
  import { setContext } from "svelte";
  import ExpenseList from "./component/ExpenseList.svelte";
  import Navbar from "./component/Navbar.svelte";
  import expensesData from "./expenses";
  import Total from "./component/Total.svelte";
  import ExpenseForm from "./ExpenseForm.svelte";
  let expenses = [...expensesData];
  $: total = expenses?.reduce((acc, value) => {
    return (acc += value?.amount)
  }, 0)
  function removeExpense(id) {
    expenses = expenses.filter(item => item.id !== id);
  }

  function edit(event) {
    const { id } = event.detail;
    // edit logic
  }

  function clearExpenses() {
    expenses = [];
  }

  const contextObj = {
    remove: removeExpense,
    // other context props
  }

  setContext('context', contextObj);
</script>

<Navbar />
<main class="main" >
  <ExpenseForm />
  <Total title="Total amount" {total} />
  <ExpenseList {expenses} on:edit={edit} />
  <button
    type="button"
    class={`btn btn-primary btn-block ${expenses.length ? '' : 'disabled'}`}
    disabled={!expenses.length}
    on:click={clearExpenses}
  >
    Clear All Expenses
  </button>
</main>
