<script>
  import ExpenseList from "./component/ExpenseList.svelte";
import Navbar from "./component/Navbar.svelte";
  import expensesData from "./expenses";
  let expenses = [...expensesData];
  function removeExpense(id) {
    expenses = expenses.filter(item => item.id !== id);
  }
</script>

<Navbar />
<main class="main" >
  <ExpenseList {expenses} {removeExpense} />
</main>
