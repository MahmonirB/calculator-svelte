<script>
  import { setContext } from "svelte";
  import ExpenseList from "./component/ExpenseList.svelte";
  import Navbar from "./component/Navbar.svelte";
  import expensesData from "./expenses";
  let expenses = [...expensesData];
  function removeExpense(id) {
    expenses = expenses.filter(item => item.id !== id);
  }
  const contextObj = {
    remove: removeExpense,
    edit: null,
  }
  setContext('context', contextObj);
</script>

<Navbar />
<main class="main" >
  <ExpenseList {expenses} />
</main>
