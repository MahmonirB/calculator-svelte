<script>
  import { setContext, onMount, onDestroy, afterUpdate } from "svelte";
  import ExpenseList from "./component/ExpenseList.svelte";
  import Navbar from "./component/Navbar.svelte";
  import Total from "./component/Total.svelte";
  import ExpenseForm from "./ExpenseForm.svelte";
  import Modal from "./component/Modal.svelte";

  let selectedExpense;
  let showForm = false;
  let expenses = [];
  $: total = expenses?.reduce((acc, value) => {
    return (acc += value?.amount)
  }, 0);

  function saveExpenses() {
    localStorage.setItem('expenses', JSON.stringify(expenses));
  }

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
    handleClose();
  }

  function addExpense({ name, amount}) {
    const newExpense = { name, amount, id: Math.random() * Date.now() };
    expenses = [newExpense, ...expenses];
    handleClose();
  }

  function modifyExpense({ name, amount, id }) {
    expenses = expenses?.map(item => {
      return item?.id === id ? {...item, name, amount} : {...item}
    });
    handleClose();
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

  onMount(() => {
    const expensesValue = localStorage.getItem('expenses');
    if (expensesValue) {
      expenses = JSON.parse(expensesValue);
    }
  });

  afterUpdate(() => { 
    saveExpenses();
  });

  onDestroy(() => { 
    saveExpenses();
  });

</script>

<Navbar />
<main class="main" >
  {#if showForm}
    <Modal>
      <ExpenseForm
        name={selectedExpense?.name}
        amount={selectedExpense?.amount}
        id={selectedExpense?.id}/>
    </Modal>
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