<script>
  import { getContext } from "svelte";
  import Title from "./component/Title.svelte";
  import { beforeUpdate, afterUpdate, onMount, onDestroy } from "svelte";
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

  onMount(() => console.log("---- on mount -----"));
  onDestroy(() => console.log("---- on destroy -----"));
  beforeUpdate(() => console.log("---- before update -----"));
  afterUpdate(() => console.log("---- after update -----"));
</script>

<section class="form">
    <Title title={isEditting ? "Edit Expense" : "Add expense"} />
    <form class="expense-form" on:submit|preventDefault={isEditting ? handleEditSubmit : handleSubmit}>
        <div class="form-control">
            <label for="name">name</label>
            <input type="text" id="name" bind:value={name}>
        </div>
        <div class="form-control">
            <label for="amount">amount</label>
            <input type="number" id="amount" bind:value={amount}>
        </div>
        {#if isEmpty}
        <p class="form-empty">
            Please fill out form fields
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
        <button class="close-btn" on:click={close}>
            <i class="fas fa-times"/>
            close
        </button>
    </form>
</section>