<script>
    import { createEventDispatcher, getContext } from "svelte";
  import { fly, slide } from "svelte/transition";
  import { quadOut, quintIn } from 'svelte/easing';
    export let name = '';
    export let amount = 0;
    export let id;
    let displayAmount = false;
    const dispatch = createEventDispatcher();
    const { remove: removeExpense } = getContext('context');
    function toggleAmount() { displayAmount = !displayAmount; }
</script>

<article class="single-expense">
    <div class="expense-info">
        <h2>{name}
        <button class="amount-btn" on:click={toggleAmount}>
            <i class="fas fa-caret-down"/>
        </button>
    </h2>
    {#if displayAmount}
        <h4 transition:slide>amount: ${amount}</h4>
    {/if}
    </div>
    <div class="expense-buttons">
        <button class="expense-btn edit-btn" on:click={() => dispatch('edit', { id })}>
            <i class="fas fa-pen" ></i>
        </button>
        <button class="expense-btn delete-btn" on:click={removeExpense(id)}>
            <i class="fas fa-trash"></i>
        </button>
    </div>
</article>

