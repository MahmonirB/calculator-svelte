<script>
  import Title from "./component/Title.svelte";


</script>

<section class="form">
    <Title title="Add expense" />
    <form class="expense-form">
        <div class="form-control">
            <label for="name">name</label>
            <input type="text" id="name">
        </div>
        <div class="form-control">
            <label for="amount">amount</label>
            <input type="text" id="amount">
        </div>
        <p class="form-empty">
            Please fill out form fields
        </p>
        <button type="submit" class="btn btn-block">
            Add Expense
        </button>
        <button class="close-btn">
            <i class="fas fa-times"/>
            close
        </button>
    </form>
</section>