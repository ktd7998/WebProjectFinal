<script>
</script>

<div class="modal-container">
    <div class="modal-content">
        <slot />
    </div>
</div>

<style>
    .modal-container {
        background-color: #00000069;
        position: absolute;
        width: 100%;
        height: 100%;
        top: 0;
        left: 0;
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .modal-content {
        background-color: white;
        width: fit-content;
    }
</style>
