<script>
  import Expense from "./Expense.svelte";
  import Title from "./Title.svelte";
    export let expenses = [];
</script>

<style>
    h2 {
        text-transform: capitalize;
    }
</style>

<section>
  <Title title="Expense title" />
  <ul>
    {#each expenses as item, index}
      <Expense {...item} on:edit />
    {:else}
      <h2>no exoenses added to the list</h2>
    {/each}
  </ul>
</section>