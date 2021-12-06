<script>
    import Title from "./Title.svelte";
    export let name = "";
    export let amount = null;
    export let isEditing;
    export let editExpense;
    export let addExpense;
    export let hideForm;

    $: isEmpty = !name || !amount;
    function handleSubmit() {
        if (isEditing) {
            editExpense({ name, amount });
        } else {
            addExpense({ name, amount });
        }
        name = "";
        amount = null;
        hideForm();
    }
</script>

<section class="form">
    <Title title="Add Expense" />
    <form class="expense-form" on:submit|preventDefault={handleSubmit}>
        <div class="form-control">
            <label for="name">Name</label>
            <input type="text" id="name" bind:value={name} />
        </div>
        <div class="form-control">
            <label for="amount">Amount</label>
            <input type="number" id="amount" bind:value={amount} />
        </div>
        {#if isEmpty}
            <p class="form-empty">Please Fill Out Both Fields</p>
        {/if}
        <button
            type="submit"
            class="btn btn-block"
            class:disabled={isEmpty}
            disabled={isEmpty}
        >
            {#if isEditing}Edit Expense{:else}Add Expense
            {/if}
        </button>
        <button type="button" class="close-btn" on:click={hideForm}>
            Close
        </button>
    </form>
</section>

<style>
    button {
        background: black;
        color: ivory;
        border: 0;
        cursor: pointer;
        border-radius: 6px;
        padding: 8px 12px;
        font-weight: bold;
        box-shadow: 1px 2px 3px black;
    }
    .form-empty {
        color: rgb(211, 42, 42);
    }
    .form {
        width: 375px;
        height: 350px;
        display: inline-block;
    }
</style>
