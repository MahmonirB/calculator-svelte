<script>
  import { setContext } from "svelte";
  import ExpenseList from "./component/ExpenseList.svelte";
  import Navbar from "./component/Navbar.svelte";
  import expensesData from "./expenses";
  import Total from "./component/Total.svelte";
  import ExpenseForm from "./ExpenseForm.svelte";
  let selectedExpense;
  let showForm = true;
  let expenses = [...expensesData];
  $: total = expenses?.reduce((acc, value) => {
    return (acc += value?.amount)
  }, 0)
  function removeExpense(id) {
    expenses = expenses.filter(item => item.id !== id);
  }

  function editExpense(event) {
    const { id } = event.detail;
    showForm = true;
    selectedExpense = expenses?.find(element => element.id === id);
  }

  function clearExpenses() {
    expenses = [];
  }

  function addExpense({ name, amount}) {
    const newExpense = { name, amount, id: Math.random() * Date.now() };
    expenses = [newExpense, ...expenses];
  }

  function modifyExpense({ name, amount, id }) {
    expenses = expenses?.map(item => {
      return item?.id === id ? {...item, name, amount} : {...item}
    });
  }
  const handleClose = () => {
    showForm = false;
  }
  const handleOpen = () => {
    showForm = true;
    selectedExpense = { name: '', amount: '', id: '' };
  }

  const contextObj = {
    remove: removeExpense,
    add: addExpense,
    modify: modifyExpense,
    close: handleClose,
    open: handleOpen,
  }

  setContext('context', contextObj);
</script>

<Navbar />
<main class="main" >
  {#if showForm}
    <ExpenseForm
      name={selectedExpense?.name}
      amount={selectedExpense?.amount}
      id={selectedExpense?.id}/>
    {/if}
  <Total title="Total amount" {total} />
  <ExpenseList {expenses} on:edit={editExpense} />
  <button
    type="button"
    class="btn btn-primary btn-block"
    class:disabled={!expenses.length}
    disabled={!expenses.length}
    on:click={clearExpenses}
  >
    Clear All Expenses
  </button>
</main>
