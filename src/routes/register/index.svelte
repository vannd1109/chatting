<!-- 
    Created by Duy Van Nguyen
    Date: 29/06/2022
 -->
<script>
	// @ts-nocheck

	let email = '';
	let password = '';
	let phone = '';
	let isValidEmail = false;
	let isValidPassword = false;
	let isValidPhone = false;
	let isShowPassword = false;
	let typePassword = 'password';
	let isPhoneEmail = true;
	let errors = {};
	let forms = [
		{
			isPhoneEmail: true,
			title: 'Đăng ký theo SĐT'
		},
		{
			isPhoneEmail: false,
			title: 'Đăng ký bằng Email'
		}
	];

	const handleValidate = () => {
        if (isPhoneEmail) {
            return isValidPhone = phone === '' ? true : false;
            
        } else {
            isValidEmail = email === '' ? true : false;
		    isValidPassword = password === '' ? true : false;
            return {
                isValidEmail,
                isValidPassword
            }
        }
    }

	const handleChangePassword = (event) => {
		password = event.target.value;
	};

	$: type = isShowPassword ? 'text' : 'password';

	const handleChangeFrom = (form) => {
		isPhoneEmail = form.isPhoneEmail;
        if(isPhoneEmail) {
            isValidEmail = false;
            isValidPassword = false;
        }else {
            isValidPhone = false;
        }
	};
</script>

<div class="relative w-screen h-screen bg-secondary ring-8">
	<div
		class="min-w-[400px] p-4 fixed min-h-[300px] left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2 bg-white"
	>
		<h6 class="uppercase font-bold text-danger text-center text-2xl">Đăng ký tài khoản</h6>
		<div class="mt-4 border-t-[1px] border-danger pt-2">
			<ul class="flex gap-4 items-center justify-center">
				{#each forms as form}
					<li
						class={`p-3 rounded-2xl flex items-center cursor-pointer border border-danger text-danger ${
							form.isPhoneEmail === isPhoneEmail ? 'bg-danger text-white' : ''
						}`}
						on:click={() => handleChangeFrom(form)}
					>
						<a href="/register" class="text-xs">{form.title}</a>
					</li>
				{/each}
			</ul>
		</div>
		<div class="main-form mt-2">
			<form class="flex flex-col gap-4" on:submit|preventDefault={handleValidate}>
				{#if isPhoneEmail}
					<div class="flex flex-col gap-2">
						<label class="text-link text-xs" for="phone">Số điện thoại</label>
						<div class="flex">
							<span
								class={`material-icons-outlined ${
									isValidEmail ? 'border-danger border-r-0' : ''
								} text-xl text-link border rounded-tl-md rounded-bl-md flex items-center p-2 bg-default`}
							>
								smartphone
							</span>
							<input
								class={`outline-none border ${
									isValidEmail ? 'border-danger' : ''
								} text-xs p-2 bg-default rounded-tr-md rounded-br-md w-full`}
								id="phone"
								type="text"
								placeholder="Nhập số điện thoại"
								bind:value={email}
							/>
						</div>
						{#if isValidPhone}
							<small class="text-xs italic text-danger">Vui lòng nhập SĐT</small>
						{/if}
					</div>
				{:else}
					<div class="flex flex-col gap-2">
						<label class="text-link text-xs" for="email">Email:</label>
						<div class="flex">
							<span
								class={`material-icons-outlined ${
									isValidEmail ? 'border-danger border-r-0' : ''
								} text-xl border text-link rounded-tl-md rounded-bl-md flex items-center p-2 bg-default`}
							>
								email
							</span>
							<input
								class={`outline-none border ${
									isValidEmail ? 'border-danger' : ''
								} text-xs p-3 bg-default rounded-tr-md rounded-br-md w-full`}
								id="email"
								type="text"
								placeholder="Nhập email"
								bind:value={email}
							/>
						</div>
						{#if isValidEmail}
							<small class="text-xs italic text-danger">Vui lòng nhập email</small>
						{/if}
					</div>
					<div class="flex flex-col gap-2">
						<label class="text-link text-xs" for="password">Mật khẩu:</label>
						<div class="flex relative">
							<span
								class={`material-icons-outlined ${
									isValidPassword ? 'border-danger border-r-0' : ''
								} text-xl border rounded-tl-md text-link rounded-bl-md flex items-center p-2 bg-default`}
							>
								vpn_key
							</span>
							<input
								class={`outline-none border w-full p-3 ${
									isValidPassword ? 'border-danger' : ''
								} text-xs bg-default rounded-tr-md rounded-br-md`}
								id="password"
								placeholder="Nhập mật khẩu"
								{type}
								{password}
								on:input={handleChangePassword}
							/>
							{#if isShowPassword}
								<span
									class="material-icons-outlined absolute right-2 text-link text-lg cursor-pointer top-1/2 -translate-y-1/2"
									on:click={() => (isShowPassword = false)}
								>
									visibility
								</span>
							{:else}
								<span
									class="material-icons-outlined absolute right-2 cursor-pointer text-lg text-link top-1/2 -translate-y-1/2"
									on:click={() => (isShowPassword = true)}
								>
									visibility_off
								</span>
							{/if}
						</div>
						{#if isValidPassword}
							<small class="text-xs italic text-danger">Vui lòng nhập mật khẩu</small>
						{/if}
					</div>
                    <div class="flex flex-col gap-2">
						<label class="text-link text-xs" for="password">Nhập lại mật khẩu:</label>
						<div class="flex relative">
							<span
								class={`material-icons-outlined ${
									isValidPassword ? 'border-danger border-r-0' : ''
								} text-xl border rounded-tl-md text-link rounded-bl-md flex items-center p-2 bg-default`}
							>
								vpn_key
							</span>
							<input
								class={`outline-none border w-full p-3 ${
									isValidPassword ? 'border-danger' : ''
								} text-xs bg-default rounded-tr-md rounded-br-md`}
								id="password"
								placeholder="Nhập lại mật khẩu"
								{type}
								{password}
								on:input={handleChangePassword}
							/>
							{#if isShowPassword}
								<span
									class="material-icons-outlined absolute right-2 text-link text-lg cursor-pointer top-1/2 -translate-y-1/2"
									on:click={() => (isShowPassword = false)}
								>
									visibility
								</span>
							{:else}
								<span
									class="material-icons-outlined absolute right-2 cursor-pointer text-lg text-link top-1/2 -translate-y-1/2"
									on:click={() => (isShowPassword = true)}
								>
									visibility_off
								</span>
							{/if}
						</div>
						{#if isValidPassword}
							<small class="text-xs italic text-danger">Vui lòng nhập mật khẩu</small>
						{/if}
					</div>
				{/if}
				<div class="flex justify-center">
					<button
						type="submit"
						class="bg-secondar border transition-all rounded-sm uppercase font-bold p-3 text-danger hover:bg-danger hover:text-white"
					>
						Đăng ký
					</button>
				</div>
				<hr class="bg-secondary m-1" />
				<div class="text-center">
					<p class="text-sm">
						Bạn đã có tài khoản?
						<a href="/login" class="text-sm text-danger hover:underline">đăng nhập</a>
						ngay
					</p>
				</div>
			</form>
		</div>
	</div>
</div>
