<script>
    import { createEventDispatcher } from 'svelte';

    const dispatch = createEventDispatcher();

    const handleHiddenModalOptions = () => {
        dispatch('onHiddenModalOptions','');
    }
</script>

<div class="modal-options">
    <div 
        class="modal-options-hidden"
        on:click={handleHiddenModalOptions}
    />
    <div class="modal-options-body">
        <slot />
    </div>
</div>

<style>
    .modal-options {
        position: relative;
    }

    .modal-options-hidden {
        position: fixed;
        width:100vw;
        height: 100vh;
		background-color: rgba(211, 191, 191, 0.034);
        z-index: 1;
        top: 0;
        left: 4rem;
    }

    .modal-options-body {
        background-color: var(--color-white);
        box-shadow: var(--box-shadow);
        min-width: 18rem;
        min-height: 10rem;
        position: absolute;
        top: 1.8rem;
        left: 4rem;
        transform: translateY(-50%);
        z-index: 100;
        cursor: default;
        color: var(--color-black);
    }
</style>