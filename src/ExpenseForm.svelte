<script>
  import Title from "./component/Title.svelte";
  let name = '';
  let amount = '';
  $: isEmpty = !name || !amount;
</script>

<section class="form">
    <Title title="Add expense" />
    <form class="expense-form">
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
            Add Expense
        </button>
        <button class="close-btn">
            <i class="fas fa-times"/>
            close
        </button>
    </form>
</section>