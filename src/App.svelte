<script>
  import { setContext } from "svelte";
  import ExpenseList from "./component/ExpenseList.svelte";
  import Navbar from "./component/Navbar.svelte";
  import expensesData from "./expenses";
  let expenses = [...expensesData];
  function removeExpense(id) {
    expenses = expenses.filter(item => item.id !== id);
  }
  function edit(event) {
    const { id } = event.detail;
    console.log("edit: " + id);
    // edit logic
  }
  const contextObj = {
    remove: removeExpense,
    // other context props
  }
  setContext('context', contextObj);
</script>

<Navbar />
<main class="main" >
  <ExpenseList {expenses} on:edit={edit} />
</main>
