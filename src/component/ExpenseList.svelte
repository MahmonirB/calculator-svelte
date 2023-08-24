<script>
  import { fly } from "svelte/transition";
  import Expense from "./Expense.svelte";
  import Title from "./Title.svelte";
  import { flip } from "svelte/animate";
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
    {#each expenses as item, index (item.id)}
    <div
      in:fly={{ x: 200, delay: (index + 1) * 400}}
      out:fly={{ x: -200 }}
      animate:flip
    >
      <Expense {...item} on:edit />
    </div>
    {:else}
      <h2>No Exoenses Added To The List</h2>
    {/each}
  </ul>
</section>