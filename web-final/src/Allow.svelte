<script>
    export let allowed = "0";
    export let total;
</script>

<h1 class:over={total > allowed}>Total Allowed: ${allowed}</h1>
<br />

<input bind:value={allowed} />

<style>
    .over {
        background-color: rgb(211, 42, 42);
        display: inline-block;
    }
</style>
