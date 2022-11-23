<script>
// @ts-nocheck
import { onMount } from "svelte";


	// @ts-nocheck
	export let isEmpty;
	export let data;
	export let timeout = 100;
	export let progress = 20;
	export let position = 3;
	export let tableHead;
	let oldPosition = position;
	let table;
	let idx = 0;
	let keyList = [];
	let total = 0;
	let newTimeout = 50;
	let newPregress = 20;

	onMount(() => {
		keyList = data.splice(2);
	});

	const handleScrollLeft = () => {
		clearInterval(idx);
		idx = setInterval(() => {
			table.scrollLeft += progress;
		}, timeout);
	};

	const handleScrollRight = () => {
		clearInterval(idx);
		idx = setInterval(() => {
			table.scrollLeft -= progress;
		}, timeout);
	};

	const handleLeave = () => {
		clearInterval(idx);
	};

	const handleChangePosition = (event) => {
		total = 0;
		oldPosition = position;
		const {value} = event.target;
		position = value;

		for (let index = oldPosition; index < position; index++) {
			total += tableHead?.children[index].offsetWidth;
		}
		table.scrollLeft = total;
	}

	const handleChangeTimeout = (event) => {
		const { value } = event.target;
		newTimeout = value;
	}

	const handleChangeProgress = (event) => {
		const { value } = event.target;
		newPregress = value;
	}

	const handleApply = () => {
		console.log(newTimeout, newPregress);
		timeout = newTimeout;
		progress = newPregress;
	}

</script>

<div class="container">
	<div class="option-list">
		<div class="select-item">
			<label class="select-label" for="timeout">Thời gian:</label>
			<input class="select-input" on:input={handleChangeTimeout} bind:value={timeout} id="timeout" type="number"/>
		</div>
		<div class="select-item">
			<label class="select-label" for="progress">Tiến độ:</label>
			<input class="select-input" on:input={handleChangeProgress} bind:value={progress} id="progress" type="number"/>
		</div>
		<!-- <div class="select-item">
			<label class="select-label" for="position">Vị trí bắt đầu:</label>
			<select 
				class="select-options"
				on:change={handleChangePosition}
			>
				{#each keyList as keyItem }
					<option disabled value={keyItem.id}>{keyItem.title}</option>
				{/each}
			</select>
		</div> -->
		<div class="select-item">
			<button class="btn" on:click={handleApply}>Áp dụng</button>
		</div>
	</div>
	<div class="table-box" bind:this={table}>
		<slot />
		{#if isEmpty}
			<p class="table-error">Không có dữ liệu phù hợp</p>
		{/if}
	</div>
	{#if !isEmpty}
		<div class="table-left" on:mouseenter={handleScrollLeft} on:mouseleave={handleLeave}>
			<span class="material-icons-outlined"> arrow_back </span>
		</div>
		<div class="table-right" on:mouseenter={handleScrollRight} on:mouseleave={handleLeave}>
			<span class="material-icons-outlined"> arrow_forward </span>
		</div>
	{/if}
</div>

<style>
	.container {
		margin: 0 auto;
		position: relative;
		overflow: hidden;
	}

	.option-list {
		display: flex;
		justify-content: flex-end;
		margin: 1rem 0;
		gap: 1rem;
		padding-right: 2rem;
	}

	.select-item {
		gap: .5rem;
		display: flex;
		align-items: center;
	}

	.select-label {
		font-size: .8rem;
		color: #888;
	}

	.select-input {
		outline: none;
		border: 1px solid #979797;
		padding: .4rem;
		border-radius: .5rem;
		font-size: .8rem;
		width: 100px;
	}

	.select-options {
		border: 1px solid #979797;
		border-radius: .5rem;
		padding: .4rem;
		outline: none;
	}

	.table-box {
		background-color: #e0e0e0;
		color: black;
		min-height: 10rem;
		max-height: 30rem;
		overflow: auto;
		width: 100%;
		position: relative;
	}

	.table-left,
	.table-right {
		position: absolute;
		width: 3em;
		height: 3em;
		z-index: 90;
		top: 50%;
		transform: translateX(-50%);
		border-radius: 1rem;
		display: flex;
		justify-content: center;
		align-items: center;
		border: 1px solid #a4a4a4;
		background-color: #e0e0e0;
		cursor: pointer;
		opacity: 0;
	}

	.container:hover .table-left {
		animation: leftToRight 0.4s forwards;
	}

	@keyframes leftToRight {
		0% {
			opacity: 0;
			left: -100%;
		}

		100% {
			left: 6rem;
			opacity: 1;
		}
	}

	.container:hover .table-right {
		animation: rightToLeft 0.4s forwards;
	}

	@keyframes rightToLeft {
		0% {
			opacity: 0;
			right: -100%;
		}

		100% {
			opacity: 1;
			right: 4rem;
		}
	}

	.table-error {
		position: absolute;
		top: calc(50% + 1em);
		left: 50%;
		transform: translateX(-50%) translateY(-50%);
		color: #979797;
		font-style: italic;
	}

	/* scrollbar */
	::-webkit-scrollbar {
		width: 1rem;
	}

	::-webkit-scrollbar-track {
		background: #f1f1f1;
	}

	::-webkit-scrollbar-thumb {
		background: #888;
	}

	::-webkit-scrollbar-thumb:hover {
		background: #555;
	}

	/* Button */
	.btn {
		border: 1px solid #979797;
		font-size: .8rem;
		padding: 0.4rem;
		border-radius: .5rem;
		font-weight: 600;
		transition: .4s;
		text-transform: uppercase;
	}

	.btn:hover {
		background-color: #979797;
		color: white;
	}

	@media (prefers-color-scheme: dark) {
		.table-box {
			color: white;
		}

		.tbody tr:nth-child(2n + 1),
		.tbody tr:nth-child(2n + 1) td:first-child,
		.tbody tr:nth-child(2n + 1) td:nth-child(2),
		.tbody tr:nth-child(2n + 1) td:nth-child(3) {
			background-color: rgb(25, 82, 90);
		}

		.thead tr th,
		.table-box,
		.tbody tr:nth-child(2n) td:first-child,
		.tbody tr:nth-child(2n) td:nth-child(2),
		.tbody tr:nth-child(2n) td:nth-child(3) {
			background-color: rgb(67, 144, 154);
		}

		.table-error {
			color: white;
		}
	}
</style>
