<script>
  import Expense from "./Expense.svelte";
    export let expenses = [];
</script>

<style>
    h2 {
        text-transform: capitalize;
    }
</style>

<section>
    {#each expenses as item, index}
      <Expense {...item} on:edit />
    {:else}
      <h2>List is empty</h2>
    {/each}
</section>