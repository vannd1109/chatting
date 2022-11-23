<!-- 
    Created by Duy Van Nguyen
    Date: 28/06/2022
 -->
<script>
    // @ts-nocheck
        let email = '';
        let password = '';
        let isValidEmail = false;
        let isValidPassword = false;
        let isShowPassword = false;
        let isError = false;
        let errors = {};
    
        const handleValidate = () => {
            isValidEmail = email === '' ? true : false;
            isValidPassword = password === '' ? true : false;
    
            return {
                isValidEmail,
                isValidPassword
            };
        };
    
        const handleChangePassword = ( event ) => {
            password = event.target.value;
            isValidPassword = password ? false : true;
        }

        const handleChangeEmail = () => {
            isValidEmail = email ? false : true;
        }
    
        $: type = isShowPassword ? 'text' : 'password';
    </script>
    
    <div class="relative w-screen h-screen bg-secondary ring-8">
        <div
            class="min-w-[400px] p-8 fixed min-h-[300px] left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2 bg-white"
        >
            <h6 class="uppercase font-bold text-danger text-center text-2xl">Đăng nhập hệ thống</h6>
            <div class="main-form mt-6">
                <form class="flex flex-col gap-4" on:submit|preventDefault={handleValidate}>
                    <div class="flex flex-col gap-2">
                        <label class="text-link text-xs" for="email">SĐT/Email</label>
                        <div class="flex">
                            <span
                                class={`material-icons-outlined ${
                                    isValidEmail ? 'border-danger' : ''
                                } text-xl text-link border rounded-tl-md rounded-bl-md flex items-center p-2 bg-default`}
                            >
                                email
                            </span>
                            <input
                                class={`outline-none border border-l-0 ${
                                    isValidEmail ? 'border-danger' : ''
                                } p-3 bg-default text-xs rounded-tr-md rounded-br-md w-full`}
                                id="text"
                                type="text"
                                placeholder="Nhập SĐT/Email"
                                bind:value={email}
                                on:input={handleChangeEmail}
                            />
                        </div>
                        {#if isValidEmail}
                            <small class="text-xs italic text-danger">Vui lòng nhập email</small>
                        {/if}
                    </div>
                    <div class="flex flex-col gap-2">
                        <label class="text-link text-xs" for="password">Mật khẩu</label>
                        <div class="flex relative">
                            <span
                                class={`material-icons-outlined ${
                                    isValidPassword ? 'border-danger' : ''
                                } text-xl text-link border rounded-tl-md rounded-bl-md flex items-center p-2 bg-default`}
                            >
                                vpn_key
                            </span>
                            <input
                                class={`outline-none border border-l-0 w-full p-3 ${
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
                                    class="material-icons-outlined text-xl text-link absolute right-2 cursor-pointer top-1/2 -translate-y-1/2"
                                    on:click={() => (isShowPassword = false)}
                                >
                                    visibility
                                </span>
                            {:else}
                                <span
                                    class="material-icons-outlined text-xl absolute text-link right-2 cursor-pointer top-1/2 -translate-y-1/2"
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
                    <div class="flex items-center justify-between gap-2">
                        <div class="flex items-center gap-1">
                            <input id="remember" type="checkbox" />
                            <label class="text-xs text-link italic cursor-pointer hover:text-black" for="remember"
                                >Ghi nhớ</label
                            >
                        </div>
                        <a href="/" class="text-link text-xs hover:text-danger hover:underline">Quên mật khẩu</a>
                    </div>
                    {#if isError}
                        <small class="text-danger italic flex justify-center font-bold">Tên đăng nhập hoặc mật khẩu không đúng!</small>
                    {/if}
                    <div class="flex justify-center">
                        <button
                            type="submit"
                            class="bg-secondar border transition-all rounded-sm uppercase font-bold p-3 text-danger hover:bg-danger hover:text-white"
                        >
                            Đăng nhập
                        </button>
                    </div>
                    <hr class="bg-secondary m-1" />
                    <div class="text-center">
                        <p class="text-sm">
                            Bạn chưa có tài khoản?
                            <a href="/register" class="text-sm text-danger underline hover:underline">đăng ký</a>
                            ngay
                        </p>
                    </div>
                </form>
            </div>
        </div>
    </div>
    