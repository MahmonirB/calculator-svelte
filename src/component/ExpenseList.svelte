<script>
  import Expense from "./Expense.svelte";
    import Title from "./Title.svelte";
    export let expenses = [];
    export let removeExpense;
</script>

<style>
    h2 {
        text-transform: capitalize;
    }
</style>

<section>
    {#each expenses as item, index}
      <Expense {...item} {removeExpense} />
    {:else}
      <h2>List is empty</h2>
    {/each}
</section>