<script>
    import { createEventDispatcher } from 'svelte';

	export let label = 'Button';
	export let icon = 'save';
    export let reverse = 'active';
    export let bg = 'seconday';
    export let isFullWidth = 'inactive';
    export let isSmallBorderRadius = 'inacvive';
    export let size = 'normal';
    export let isbBorderRadiusCircle = 'inactive';
    export let classButton = '';
    let dispatch = createEventDispatcher();

    const handleClick = () => {
        dispatch('onClick','');
    }
</script>

<button 
    class={`btn btn-reverse-${reverse} ${classButton} btn-border-radius-circle--${isbBorderRadiusCircle} btn-${bg} btn-fullWidth-${isFullWidth} btn-small-radius-${isSmallBorderRadius}`}
    on:click={handleClick}
>
    {#if icon}
        <span class="material-icons-outlined btn-icon">
            {icon}
        </span>
    {/if}
    {#if label}
        <label class={`btn-label btn-label--${size}`} for="">
            {label}
        </label>
    {/if}
</button>

<style>
	.btn {
		display: flex;
		overflow: hidden;
		border-radius: 0.5rem;
		padding: var(--padding);
        transition: .4s;
	}

    .btn-reverse-active {
        flex-direction: row-reverse;
    }

    .btn-border-radius-circle--active {
        border-radius: 2.5rem;
    }

    .btn-hover:hover {
		transition: 0.4s;
		background-color: var(--color-gray-second);
	}

    .btn-fullWidth-active {
        width: 100%;
        justify-content: center;
        padding: 1rem;
    }

    .btn-small-radius-active {
        border-radius: 0.2rem;
    }

    .btn-active {
        background-color: rgba(0, 0, 0, 0.084);
        border-radius: unset;
    }

    .btn-secondary {
        background-color: var(--color-gray-second) !important;
    }

    .btn-secondary:hover {
        transition: .4s;
        background-color: var(--color-gray-hover) !important;
    }

    .btn-info {
        background-color: var(--color-info);
        color: var(--color-white);
    }

    .btn-info:hover {
        transition: .4s;
        background-color: var(--color-info-hover) !important;
    }

    .btn-danger {
        background-color: var(--color-danger) !important;
        color: var(--color-white) !important;
    }

    .btn-danger:hover {
        background-color: var(--color-danger-hover) !important;
        color: var(--color-white);
    }

    .btn-warning {
        background-color: var(--color-warning);
        color: var(--color-white);
    }

    .btn-warning:hover {
        background-color: var(--color-warning-hover) !important;
    }

	.btn-icon {
		font-size: 1.2rem;
        line-height: 1.2rem;
	}

	.btn-label {
        cursor: pointer;
        font-size: .9rem;
        font-weight: 600;
	}

    .btn-label--small {
        font-size: .8rem;
    }
</style>
