<script>
    import Title from "./Title.svelte";
    export let expenses = [];
</script>

<section>
    {#each expenses as item}
    <Title title={item.name} />
    {/each}
</section>