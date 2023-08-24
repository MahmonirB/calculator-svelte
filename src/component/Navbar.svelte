<script>
  import { getContext } from "svelte";
  const { open } = getContext('context');
</script>

<nav class="nav">
    <div class="nav-center">
      <h1 class="nav-title">Budget Calculator</h1>
      <button class="nav-btn" on:click={open}>
        <i class="far fa-plus-square"></i>
        Add item
      </button>
    </div>
  </nav>
  