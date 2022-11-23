<script>
    import { createEventDispatcher } from 'svelte';
    import Button from '../button/Button.svelte';

    
    let dispatch = createEventDispatcher();
    export let label = 'Label';
    export let type = 'zoom';
    export let reverse = 'inactive';
    let bgBtnSecondary = 'secondary';
    let bgBtnInfo = 'info';
    let lblButtonCancel = 'Hủy';
    let iconButton = '';
    let lblButtonApply = 'Xác nhận';
// @ts-nocheck
    const handleHiddenModal = () => {
        dispatch('onHidden');
    }

    const handleApply = () => {
        dispatch('onHidden');
    }
</script>
    <div 
        class="modal">
        <div 
            class="modal-hidden"
            on:click={handleHiddenModal}
        />
		<div class={`modal-body modal-${type}`}>
            <div class={`modal-header modal-header-reverse-${reverse}`}>
                <label class="modal-header--label" for="">
                    {label}
                </label>
                <span 
                    class="material-icons-outlined modal-header--icon"
                    on:click={handleHiddenModal}
                >
                    close
                </span>
            </div>
            <hr class="preparator"/>
            <div class="modal-content">
                <div class="modal-content-main">
                    <slot />
                </div>
                <div class="modal-btn">
                    <Button 
                        label={lblButtonCancel}
                        icon={iconButton}
                        bg={bgBtnSecondary}
                        on:onClick={handleHiddenModal}
                    />
                    <Button 
                        label={lblButtonApply}
                        icon={iconButton}
                        bg={bgBtnInfo}
                        on:onClick={handleApply}
                    />
                </div>
            </div>
        </div>
	</div>
<style>
	.modal {
		position: fixed;
		width: 100vw;
		height: 100vh;
	}

    .modal-hidden {
        position: fixed;
		width: 100vw;
		height: 100vh;
		background-color: rgba(211, 191, 191, 0.034);
        z-index: 99;
    }

	.modal-body {
        position: absolute;
        min-width: 30%;
        min-height: 50%;
        background-color: var(--color-secondary);
        z-index: 100;
        border-radius: var(--border-radius);
        box-shadow: var(--box-shadow);
        opacity: 0;
	}

    .modal-zoom {
        animation: zoom .2s forwards;
    }

    @keyframes zoom {
        0% {
            opacity: 0;
            transform: translateX(-50%) translateY(-50%) scale(0);
            top: 50%;
            left: 50%;
        }

        100% {
            opacity: 1;
            transform: translateX(-50%) translateY(-50%) scale(1);
            top: 50%;
            left: 50%;
        }
    }

    .modal-header {
        display: flex;
        justify-content: space-between;
        padding: .5rem 1rem;
        align-items: center;
    }

    .modal-header-reverse-active {
        flex-direction: row-reverse;
    }

    .modal-header--label {
        color: var(--color-black);
        font-weight: 600;
    }

    .modal-header--icon {
        cursor: pointer;
        padding: .4rem;
        border-radius: 50%;
        font-style: normal;
        color: var(--color-black);
    }

    .modal-header--icon:hover {
        transition: .2s;
        background-color: var(--color-gray-second);
        color: var(--color-danger);
    }

    .preparator {
        border-color: var(--color-gray-second);
    }

    .modal-content {
        padding: 1rem;
    }
    
    .modal-content-main {
        display: flex;
        min-height: 12rem;
    }

    .modal-btn {
        display: flex;
        justify-content: flex-end;
        flex: 1;
        gap: 1rem;
    }
</style>
