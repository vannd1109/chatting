<script>
	import TabContent from '../../components/tabs/TabContent.svelte';
	import Button from '../../components/button/Button.svelte';
	import Tabs from '../../components/tabs/Tabs.svelte';
	import DefaultLayout from '../../layouts/DefaultLayout.svelte';
	import All from './All.svelte';
	import UnRead from './UnRead.svelte';

	let isHeading = true;
	let currentTab = 1;
	let tabList = [
		{
			id: 1,
			title: 'Tất cả'
		},
		{
			id: 2,
			title: 'Chưa đọc'
		}
	];

	// @ts-ignore
	const handleChangeCurrentTab = ({ detail }) => {
		currentTab = detail;
	};
</script>

<DefaultLayout {isHeading}>
	<div class="flex justify-between p-2">
		<Tabs {tabList} {currentTab} on:onTab={handleChangeCurrentTab}>
		</Tabs>
		<div class="">
			<Button
				classButton='float-left'
				label='Phân loại' 
				reverse='active' 
				icon='expand_more'
				size='small'
				bg='hover'
				isbBorderRadiusCircle='active'
			/>
			<Button
				classButton='float-left ml-2'
				label=''
				icon='more_horiz'
				size='small'
				bg='hover'
				isbBorderRadiusCircle='active'
			/>
		</div>
	</div>
	<TabContent>
		{#if currentTab === 1}
			<All />
			{:else}
			<UnRead />
		{/if}
	</TabContent>
</DefaultLayout>

<style>
	.tab-list button {
		float: left;
	}
</style>
