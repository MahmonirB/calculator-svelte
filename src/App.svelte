<script>
  import ExpenseList from "./component/ExpenseList.svelte";
import Navbar from "./component/Navbar.svelte";
  import expensesData from "./expenses";
  let expenses = [...expensesData];
</script>

<Navbar />
<main class="main" >
  <ExpenseList {expenses} />
</main>
