<script>
	// @ts-nocheck
	import { createEventDispatcher } from 'svelte';
	import Modal from '../components/modal/Modal.svelte';
	import Button from '../components/button/Button.svelte';

	let dispatch = createEventDispatcher();
	export let avatar = 'person_add_alt';
	export let label = 'Label';
	let lblButton = '';
	let isShowModal = false;
	let modalLabel = '';
	export let isHeading = false;
	export let isShowNavTabs = false;

	const handleHiddenModal = () => {
		isShowModal = false;
	};

	const handleAddFriendToGroup = () => {
		isShowModal = true;
		modalLabel = 'Thêm thành viên';
	};

	const handleShowTabNav = () => {	
		dispatch('onNavTab','');
	}

	const handleKeyDown = (event) => {
		if (event.key === 'Escape') {
			isShowModal = false;
		}
	}
</script>

<svelte:window on:keydown={handleKeyDown} />

<div class="content">
	{#if isHeading}
		<div class="content-header">
			<div class="content-header--head">
				<span class="material-icons-outlined content-header--avatar">
					{avatar}
				</span>
				<label class="content-header--label" for="">
					{label}
				</label>
			</div>
			<div class="content-header--tail">
				<Button 
					label={lblButton} 
					icon="group_add"
					bg='hover'
					on:onClick={handleAddFriendToGroup}
				/>
				<Button 
					label={lblButton}
					icon="search"
					bg='hover'
				/>
				<Button
					label={lblButton}
					icon="videocam"
					bg='hover'
				/>
				<Button 
					label={lblButton}
				 	icon="width_wide"
					isSmallBorderRadius='active'
					on:onClick={handleShowTabNav}
					bg={`${isShowNavTabs ? 'danger' : 'hover'}`}
				/>
			</div>
		</div>
		<hr class="preparator" />
	{/if}
</div>

{#if isShowModal}
	<Modal on:onHidden={handleHiddenModal} label={modalLabel} />
{/if}

<style>
	.content {
		display: flex;
		flex: 1;
		flex-direction: column;
	}

	.content-header {
		display: flex;
		justify-content: space-between;
		height: 4rem;
		padding: 1rem;
	}

	.content-header--head {
		display: flex;
		align-items: center;
		gap: 1rem;
	}

	.content-header--avatar {
		background-color: var(--color-danger);
		color: var(--color-white);
		border-radius: 50%;
		padding: var(--padding);
	}

	.content-header--label {
		font-size: 1.2rem;
		font-weight: 600;
	}

	.content-header--tail {
		display: flex;
		gap: 0.5rem;
		align-items: center;
	}

	.preparator {
		border-color: var(--color-gray-second);
		display: flex;
	}
</style>
