<script>
  import { getContext } from "svelte";
  import Title from "./component/Title.svelte";
  export let name = '';
  export let amount = '';
  export let id = '';

  $: isEmpty = !name || !amount;
  $: isEditting = !!id;

  const { add: addExpense, modify: modifyExpense, close } = getContext('context');
  function handleSubmit() {
    addExpense({ name, amount});
    name = '';
    amount = '';
  }

  function handleEditSubmit() {
    modifyExpense({ name, amount, id});
    name = '';
    amount = '';
  }
</script>

<section class="form">
    <Title title={isEditting ? "Edit Expense" : "Add expense"} />
    <form class="expense-form" on:submit|preventDefault={isEditting ? handleEditSubmit : handleSubmit}>
        <div class="form-control">
            <label for="name">Name</label>
            <input type="text" id="name" bind:value={name}>
        </div>
        <div class="form-control">
            <label for="amount">Amount</label>
            <input type="number" id="amount" bind:value={amount}>
        </div>
        {#if isEmpty}
        <p class="form-empty">
            Please Fill Out Form Fields
        </p>
        {/if}
        <button
          type="submit"
          class="btn btn-block"
          class:disabled={isEmpty}
          disabled={isEmpty}
        >
            {isEditting ? "Edit Expense" : "Add expense"}
        </button>
    </form>
    <button class="close-btn" on:click={close}>
        <i class="fas fa-times"/>
        Close
    </button>
</section>