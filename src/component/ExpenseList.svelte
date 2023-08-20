<script>
  import { fly } from "svelte/transition";
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
    <div transition:fly={{ x: 200, delay: index * 200}}>
      <Expense {...item} on:edit />
    </div>
    {:else}
      <h2>no exoenses added to the list</h2>
    {/each}
  </ul>
</section>