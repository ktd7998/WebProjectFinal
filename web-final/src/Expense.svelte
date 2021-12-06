<script>
    import Icon from "@iconify/svelte";
    import { getContext } from "svelte";
    import { fade } from "svelte/transition";
    export let id;
    export let name = "";
    export let amount = 0;
    let displayAmount = false;

    let show = false;
    let status = false;
    let message;

    function toggleShow(theMessage) {
        show = !show;
        message = theMessage;
    }

    function toggleAmount() {
        displayAmount = !displayAmount;
    }

    const removeExpense = getContext("remove");
    const setModifiedExpense = getContext("modify");
</script>

<article class="single-expense">
    <div>
        <h2>
            {name}
            <button
                class="view-btn"
                on:click={toggleAmount}
                on:mouseenter={() => toggleShow("View")}
                on:mouseleave={toggleShow}
            >
                <Icon icon="bx:bxs-down-arrow" width="18" />
            </button>
            <button
                class="edit-btn"
                on:click={() => setModifiedExpense(id)}
                on:mouseenter={() => toggleShow("Edit")}
                on:mouseleave={toggleShow}
            >
                <Icon icon="bx:bxs-edit" width="18" />
            </button>
            <button
                class="delete-btn"
                on:click={() => removeExpense(id)}
                on:mouseenter={() => toggleShow("Delete")}
                on:mouseleave={toggleShow}
            >
                <Icon icon="mdi:trash-can" width="18" />
            </button>
            {#if displayAmount}
                <h4>amount : ${amount}</h4>
            {/if}
        </h2>
    </div>

    {#if show}
        <div
            class="guide"
            class:hidden={status}
            transition:fade={{ duration: 3000 }}
        >
            select to: {message}
        </div>
    {/if}
</article>

<style>
    h4 {
        font-size: 15px;
    }
    .guide.hidden {
        background: red;
    }
</style>
