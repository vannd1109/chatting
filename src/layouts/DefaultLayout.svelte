<script>
    import NavBar from '../components/navbar/NavBar.svelte';
    import PageContentLayout from './PageContentLayout.svelte';
    export let isHeading = false;
    export let lblHeading = 'Label';
    let isShowNavTabs = false;
    export let isNavTabs = false;
    export let lblNav = '';

    const handleShowNavTab = () => {
        isShowNavTabs = !isShowNavTabs;
    }
</script>

<div class="flex overflow-hidden">
    <NavBar isShowNavTabs={true} label={lblNav}>
        <slot />
    </NavBar>
    <PageContentLayout
        isHeading={isHeading} 
        label={lblHeading}
        on:onNavTab={handleShowNavTab}
        {isShowNavTabs}
    />
    <NavBar {isShowNavTabs} {isNavTabs} label='Thông tin hội thoại'/>
</div>