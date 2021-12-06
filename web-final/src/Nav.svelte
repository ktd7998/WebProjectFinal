<script>
    import Icon from "@iconify/svelte";
    export let showForm;
</script>

<nav class="nav">
    <div class="center">
        <h1 class="nav-title">Budget Application</h1>
        <button type="button" on:click={showForm}>
            Add Expense
            <Icon
                icon="fluent:add-circle-24-filled"
                color="blueviolet"
                width="20"
                inline={true}
            />
        </button>
    </div>
</nav>

<style>
    nav {
        background: blueviolet;
        padding: 10px;
        border: 3px solid black;
    }
    .center {
        display: flex;
        justify-content: center;
        align-items: center;
    }

    h1 {
        margin: 20px;
        text-align: center;
        color: ivory;
        font-size: xx-large;
    }
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
</style>
