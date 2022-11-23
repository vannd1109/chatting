<!-- 
    Created by Duy Van Nguyen
    Date: 14/07/2022
 -->
<script>
	// @ts-nocheck
	import { onMount } from 'svelte';
	import { goto } from '$app/navigation';
	import Input from '../input/Input.svelte';
	import Modal from '../modal/Modal.svelte';
	import Button from '../button/Button.svelte';
	import ModalOptions from '../modal-options/ModalOptions.svelte';

	let tabList = [
		{
			id: 0,
			key: 'user',
			icon: 'account_circle',
			title: 'Người dùng',
			path: '/'
		},
		{
			id: 1,
			key: 'message',
			icon: 'chat',
			title: 'Tin nhắn',
			path: '/message'
		},
		{
			id: 2,
			key: 'phone',
			icon: 'fact_check',
			title: 'Danh bạ',
			path: '/phone-book'
		},
		{
			id: 3,
			key: 'job',
			icon: 'work_outline',
			title: 'Công việc',
			path: '/job'
		},
		{
			id: 4,
			key: 'documents',
			icon: 'description',
			title: 'Tài liệu',
			path: '/documents'
		},
		{
			id: 5,
			key: 'constructions',
			icon: 'construction',
			title: 'Công cụ',
			path: '/'
		},
		{
			id: 6,
			key: 'settings',
			icon: 'settings',
			title: 'Cài đặt',
			path: '/'
		}
	];

	// button
	let lblBtnAddFriend = '';
	let lblBtnAddGroup = '';
	let isFullWidth = 'active';
	let isSmallBorderRadius = 'active';
	// tabs
	let tabObj = {
		tab_current: 1,
		tab_key: 'phone',
		tab_path: '/',
		is_show: false
	};
	let tabCurrent = 1;
	let tabPath = '';
	let tabCurrentHover;
	let tabKey;
	export let isShowNavTabs = false;
	export let isNavTabs = true;
	export let label = 'Label';
	let inputString = '';
	let isShowClose = false;
	let inputActive = false;
	let input;
	let isShowBtnSearch = false;
	let isSearchHistoryResult = false;
	// modal
	let isShowModal = false;
	let modalLabel = '';

	// modal-options
	let isShowModalOptions = false;

	onMount(() => {
		let tabObjNew = JSON.parse(localStorage.getItem('tab'));

		if (tabObjNew > '') {
			tabCurrent = parseInt(tabObjNew.tab_current);
			tabKey = tabObjNew.tab_key;
			if (tabKey === 'user' || tabKey === 'constructions' || tabKey === 'settings') {
				isShowModalOptions = tabObjNew.is_show;
			}
		} else {
			localStorage.setItem('tab', JSON.stringify(tabObj));
		}
	});

	const checkTabLocalStorage = (tabItem, tabObjItem) => {
		if (
				tabItem.key !== tabObjItem.tab_key &&
				(tabItem.key === 'constructions' || tabItem.key === 'settings' || tabItem.key === 'user')
			) {
				isShowModalOptions = true;
			} else {
				isShowModalOptions = false;
			}

			if (
				(tabItem.key === 'constructions' || tabItem.key === 'settings' || tabItem.key === 'user') &&
				tabObjItem.is_show === false
			) {
				isShowModalOptions = true;
			}

			tabObjItem.tab_key = tabItem.key;
			tabCurrent = tabItem.id;
			tabObjItem.tab_current = tabItem.id;
			tabObjItem.tab_path = tabItem.path;
			tabObjItem.is_show = isShowModalOptions;
			localStorage.setItem('tab', JSON.stringify(tabObjItem));

			if(tabItem.path !== '/') {
				goto(`${tabItem.path}`);
			}
	}

	const handleChangePage = (tab) => {
		let tabObjNew = JSON.parse(localStorage.getItem('tab'));

		if (tabObjNew === null) {
			localStorage.setItem('tab', JSON.stringify(tabObj));
			tabObjNew = JSON.parse(localStorage.getItem('tab'));

			checkTabLocalStorage(tab, tabObjNew);
		} else {
			checkTabLocalStorage(tab, tabObjNew);
		}
	};

	const handleMouseOver = (value) => {
		tabCurrentHover = value;
	};

	const handleMouseOut = () => {
		tabCurrentHover = '';
	};

	const handleAddFriend = () => {
		isShowModal = true;
		modalLabel = 'Thêm bạn';
	};

	const handleAddGroupChat = () => {
		isShowModal = true;
		modalLabel = 'Tạo nhóm';
	};

	const handleInput = ({ detail }) => {
		isShowClose = detail > '' ? true : false;
	};

	const handleFormatInput = () => {
		input.value = '';
		isShowClose = false;
		isShowBtnSearch = false;
	};
	const handleFocus = ({ detail }) => {
		isShowBtnSearch = true;
		input = detail;
	};

	const handleFocusOut = () => {
		inputActive = false;
	}

	const handleHiddenModal = () => {
		isShowModal = false;
	};

	const handleHiddenModalOptions = () => {
		isShowModalOptions = false;
		localStorage.removeItem('tab');
		tabCurrentHover = '';
	};

	const handleKeyDown = (event) => {
		if (event.key === 'Escape') {
			isShowModal = false;
			isShowClose = false;
			isShowBtnSearch = false;

			inputActive = false;
		}
	};

	const handleRefreshPage = () => {
		console.log('ok');
	};

	const handleLogOut = () => {
		isShowModal = true;
		tabObj = JSON.parse(localStorage.getItem('tab'));
		isShowModalOptions = false;
		modalLabel = 'Xác nhận'
		tabCurrentHover = '';
		tabObj.is_show = false;
		localStorage.setItem('tab', JSON.stringify(tabObj));
	}

	const handleInfomation = () => {
		isShowModal = true;
		tabObj = JSON.parse(localStorage.getItem('tab'));
		isShowModalOptions = false;
		modalLabel = 'Thông tin tài khoản'
		tabCurrentHover = '';
		tabObj.is_show = false;
		localStorage.setItem('tab', JSON.stringify(tabObj));
	}
</script>

<svelte:window on:keydown={handleKeyDown} on:reset={handleRefreshPage} />

{#if isShowNavTabs}
	<nav class="nav">
		{#if isNavTabs}
			<div class="nav-tabs">
				<ul class="nav-list">
					{#each tabList as item}
						<!-- svelte-ignore a11y-mouse-events-have-key-events -->
						<li
							class="nav-item"
							on:mouseover={() => handleMouseOver(item.id)}
							on:mouseout={handleMouseOut}
						>
							<Button
								label=""
								icon={item.icon}
								{isFullWidth}
								{isSmallBorderRadius}
								bg={item.id === tabCurrent ? 'active' : ''}
								on:onClick={() => handleChangePage(item)}
							/>
							{#if item.id === tabCurrentHover}
								<small class="nav-item--child">{item.title}</small>
							{/if}
							{#if isShowModalOptions && item.id === tabCurrent}
								<ModalOptions on:onHiddenModalOptions={handleHiddenModalOptions}>
									{#if item.key === 'user'}
										<h3 class="user_label">Duy Nguyen</h3>
										<hr class="preparator ml-4" />
										<ul class="user_list">
											<li class="user_item">
												<p 
													class="user_link"
													on:click={handleInfomation}
												>
													Hồ sơ của bạn
												</p>
											</li>
											<li class="user_item">
												<p class="user_link">Cài đặt</p>
											</li>
											<hr class="preparator ml-4" />
											<li class="user_item">
												<p 
													class="user_link"
													on:click={handleLogOut}
												>
													Đăng xuất
												</p>
											</li>
										</ul>
									{/if}
								</ModalOptions>
							{/if}
						</li>
					{/each}
				</ul>
			</div>
		{/if}
		<div class="nav-content">
			{#if label}
				<div class="nav-label">
					{label}
				</div>
			{:else}
				<div class="search">
					<Input
						label=""
						id="stringSearch"
						placeholder="Tìm kiếm..."
						on:focus={handleFocus}
						on:focusOut={handleFocusOut}
						on:value={handleInput}
						inputString={inputString}
						{isShowClose}
						inputActive={inputActive}
						input={input}
						on:value={handleInput}
					/>
					{#if isShowBtnSearch}
						<Button label="Đóng" icon="" on:onClick={handleFormatInput} bg="hover" />
					{:else}
						<Button
							label={lblBtnAddFriend}
							icon="person_add"
							on:onClick={handleAddFriend}
							bg="hover"
						/>
						<Button
							label={lblBtnAddGroup}
							icon="group_add"
							on:onClick={handleAddGroupChat}
							bg="hover"
						/>
					{/if}
				</div>
			{/if}
			{#if isShowBtnSearch}
				<div class="search-history">
					<label for="" class="search-history--label"> Tìm gần đây </label>
					<div class="search-history--result">
						{#if !isSearchHistoryResult}
							<p>Không có tìm kiếm nào gần đây</p>
						{/if}
					</div>
				</div>
			{/if}
			<hr class="preparator" />
			{#if isShowBtnSearch}
				<div class="search-filter">
					<label for="" class="search-filter--label"> Lọc tin nhắn </label>
					<div class="search-filter--btn">
						<Button
							icon=""
							label="Nhắc bạn"
							bg="secondary"
							size="small"
							isbBorderRadiusCircle="active"
						/>
						<Button
							icon=""
							label="Biểu cảm"
							bg="secondary"
							size="small"
							isbBorderRadiusCircle="active"
						/>
					</div>
				</div>
			{:else}
				<slot />
			{/if}
		</div>
	</nav>
{/if}
{#if isShowModal}
	<Modal on:onHidden={handleHiddenModal} label={modalLabel}>
			
	</Modal>
{/if}

<style>
	.nav {
		width: 24rem;
		display: flex;
		height: 100vh;
		box-shadow: 0 0 40px #d7d7d7;
	}

	.nav-tabs {
		background-color: var(--color-danger);
	}

	.nav-list {
		width: 4rem;
		height: 100vh;
		display: flex;
		flex-direction: column;
		padding: 2rem 0;
	}

	.nav-item {
		position: relative;
		width: 4rem;
		color: var(--color-white);
		z-index: 999;
		cursor: pointer;
		z-index: 10;
	}

	.nav-item:hover {
		background-color: rgba(0, 0, 0, 0.084) !important;
	}

	.nav-item--child {
		position: absolute;
		top: 50%;
		left: 100%;
		transform: translateY(-50%);
		box-shadow: var(--box-shadow);
		background-color: var(--color-white);
		color: var(--color-black);
		min-width: 6rem;
		display: flex;
		justify-content: center;
		padding: var(--padding);
		border-radius: var(--border-radius);
	}

	.nav-content {
		display: flex;
		width: 100%;
		flex-direction: column;
	}

	.search {
		display: flex;
		height: 4rem;
		align-items: center;
		gap: 0.5rem;
		padding: 1rem;
	}

	.nav-label {
		height: 4rem;
		display: flex;
		align-items: center;
		justify-content: center;
		font-weight: 600;
	}

	.search-history,
	.search-filter {
		padding: 1rem;
	}

	.search-history--label,
	.search-filter--label {
		font-weight: 500;
		font-size: 0.9rem;
	}

	.search-history--result {
		padding: 1rem 0;
	}

	.search-history--result p {
		font-size: 0.9rem;
	}

	.search-filter--btn {
		display: flex;
		gap: 1rem;
		margin-top: 1rem;
	}

	.preparator {
		border-color: var(--color-gray-second);
		display: flex;
	}

	/* USER */
	.user_label {
		padding: .5rem 1rem;
		font-weight: 600;
	}

	.user_list {
		padding-left: 0;
	}

	.user_item {
		font-size: .9rem;
	}

	.user_link {
		cursor: pointer;
		padding: .5rem 1rem;
	}

	.user_link:hover {
		background-color: var(--color-gray);
	}
</style>
