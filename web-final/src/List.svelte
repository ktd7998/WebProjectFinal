<script>
    import Title from "./Title.svelte";
    import Expense from "./Expense.svelte";
    export let expenses = [];
</script>

<section>
    <Title title="Expense List" />
    <ul>
        {#each expenses as expense, index}
            <Expense {...expense} />
        {:else}
            <h2>Your list is empty. Please add an item.</h2>
        {/each}
    </ul>
</section>

<style>
    h2 {
        font-weight: bolder;
        color: rgb(211, 42, 42);
    }
</style>
