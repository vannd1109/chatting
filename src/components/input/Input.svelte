<script>
// @ts-nocheck

    import { createEventDispatcher } from 'svelte';
    import '../css/root.css';
    export let id = 'id';
    export let label = 'Label';
    export let icon = 'search';
    export let placeholder = '';
    export let type = 'text';
    export let disabled = false;
    export let isShowClose;
    export let inputString = '';
    let dispatch = createEventDispatcher();
    export let inputActive = false;
    export let input;

    const handleFormatInput = () => {
        input.value = '';
        inputString = '';
        inputActive = true;
        isShowClose = false;
        input.focus();
    }

    const handleFocus = () => {
        inputActive = true;
        dispatch('focus',input);
    }

    const handleFocusOut = () => {
        inputActive = false;
        dispatch('focusOut',input);
    }

    const handleInput = (e) => {
        const {value} = e.target;
        inputString = value;
        dispatch('value', value);
        isShowClose = true;
    }

</script>

<div class="input-box">
    {#if label}
        <label class="input-label" for="">{label}</label>
    {/if}
    <div class={`input-control input-${inputActive ? 'active' : 'in-active'}`}>
        <span class="material-icons-outlined input-icon">
            {icon}
        </span>
        <input
            class="input"
            {id}
            {placeholder} 
            {disabled}
            {type}
            bind:this={input}
            on:focus={handleFocus}
            on:focusout={handleFocusOut}
            on:input={handleInput}
        />
        {#if isShowClose}
            <span 
                class="material-icons-outlined icon-close"
                on:click={handleFormatInput}
            >
                close
            </span>
        {/if}
    </div>
</div>

<style>
    .input-box {
        display: flex;
        flex-direction: column;
        gap: var(--gap-wh);
    }

    .input-label {
        font-size: 0.8rem;
        color: var(--color-link);
    }

    .input-control {
        display: flex;
        align-items: center;
        border: 1px solid var(--color-link);
        border-radius: 1rem;
        overflow: hidden;
        padding: .4rem .5rem;
    }

    .input-active {
        border: 1px solid var(--color-danger);
    }

    .input-icon {
        font-size: 1rem;
    }

    .input {
        outline: none;
        font-size: .85rem;
        margin: 0 .5rem;
    }

    .icon-close {
        font-size: 1rem;
        cursor: pointer;
    }
</style>