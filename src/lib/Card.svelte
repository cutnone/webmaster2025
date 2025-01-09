<script lang="ts">
    const { name, addons = null, price, imageUrl} = $props();
</script>

<div class="card">
    <img src={imageUrl} alt="">
    <div class="text-cluster">
        {#if addons}
            <h3>{name}</h3>
            <div class="row">
                <span class="addons">{addons}</span>
                <div class="price">{price}</div>
            </div>
            {:else}
            <div class="row">
                <h3>{name}</h3>
                <div class="price">{price}</div>
            </div>
        {/if}
    </div>
    <div class="row">
        <button>Add to Order</button>
    </div>
</div>

<style lang="scss">
    .card {
        border-radius: 2rem;
        padding: 1rem;
        border: .25rem solid var(--color-background-alt);
        width: 30ch;
        background-color: var(--color-background);
        box-shadow: 0 0 2rem #000000aa;
        display: flex;
        gap: .5rem;
        flex-direction: column;
        grid-column: span 1;
        grid-row: span 1;
    }
    img {
        border-radius: 1rem;
        width: 100%;
        height: 20ch;
    }

    .addons, .price {
        color: var(--color-accent);
    }

    h3 {
        font-family: var(--accent-font-family);
        font-size: 1.25rem;
        font-weight: normal;
        font-style: italic;
        color: var(--color-accent);
    }

    .row {
        display: flex;
        width: 100%;
        justify-content: space-between;
        align-items: center;
    }

    .text-cluster {
        display: flex;
        flex-direction: column;
        gap: .25rem;
        padding: .5rem;
    }

    button {
        flex-grow: 1;
        padding: .5rem 1rem;
        border-radius: 1rem;
    }

</style>