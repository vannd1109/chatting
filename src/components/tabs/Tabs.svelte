<script>
    // @ts-nocheck
        import { createEventDispatcher } from 'svelte';
        import TabContent from './TabContent.svelte';
        import TabHeader from './tabHeader.svelte';
        export let tabList;
        export let currentTab = 1;
        let dispatch = createEventDispatcher();
    
        const handleChangeCurrentTab = (id) => {
            dispatch('onTab',id)
        }
    </script>


<div class="tabs">
    <ul class="tab-list">
        {#each tabList as tabItem}
            <li 
                class={`tab-item ${tabItem.id === currentTab ? 'tab-active' : ''}`}
                on:click={() => handleChangeCurrentTab(tabItem.id)}
            >
                {tabItem?.title}
            </li>
        {/each}
    </ul>
</div>

<style>
    .tabs {
        padding: var(--padding);
        display: flex;
        flex-direction: column;
    }

    .tab-list {
        display: flex;
        gap: 1rem;
    }

    .tab-item {
        font-size: .9rem;
        padding-bottom: var(--padding);
        transition: .2s;
        border-bottom: 2px solid transparent;
        cursor: pointer;
        font-weight: 500;
        color: var(--color-link);
    }

    .tab-item:hover {
        color: var(--color-danger);
    }

    .tab-active {
        color: var(--color-danger);
        border-bottom: 2px solid var(--color-danger);
    }
</style>