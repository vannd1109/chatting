<script>
    let isEmptyMessage = true;
</script>

<div class="un-read">
    {#if isEmptyMessage}
        <div class="no-message">
            <span class="material-icons-outlined no-message--icon">
                chat_bubble_outline
            </span>
            <p class="no-message--label">Không có tin nhắn chưa đọc</p>
        </div>
    {/if}
</div>

<style>
    .un-read {
        position: relative;
        height: 100vh;
    }
    .no-message {
        position: absolute;
        top: 30%;
        transform: translateY(-30%) translateX(-50%);
        left: 50%;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        text-align: center;
        width: 100%;
    }

    .no-message--icon {
        font-size: 8rem;
        color: var(--color-gray-second);
    }

    .no-message--label {
        color: var(--color-black);
        font-size: .9rem;
    }
</style>