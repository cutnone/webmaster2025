<script lang="ts">
	import { expoOut } from "svelte/easing";
	import { slide } from "svelte/transition";


    const {items = $bindable([{
        name: "Cream of Mushroom",
        size: "Cup",
        quantity: 1,
        price: 6.99,
    }])} = $props();

    let cartSize = $derived(items.reduce((acc, v)=>acc+(v.quantity), 0))

    let subtotal = $derived(items.reduce((acc, v)=>acc+(v.price*v.quantity), 0))
    let tax = $derived(subtotal * .06);
    let total = $derived(subtotal + tax);

    let receiptOpen = $state(false);

    function toggleReceipt() {
        receiptOpen = !receiptOpen;
    }

    function closeReceipt() {
        receiptOpen = false;
    }

    function clearCart() {
        // items.splice(0, items.length);
        items.length = 0;
    }

</script>

{#if receiptOpen}
<div transition:slide={{duration: 300, easing: expoOut}} class="receipt">
    <div class="row">
        <h1>my order</h1>
        <button class="iconbtn" onclick={closeReceipt}><img src="/enoki/icon-cross.svg" alt=""></button>
    </div>
    <div class="items">
        {#each items as item, i}
            <div class="row">
                <button class="iconbtn" onclick={()=>{items.splice(i, 1)}}><img src="/enoki/icon-cross.svg" alt=""></button>
                <span>{item.name} ({item.size}) x{item.quantity}</span>
                <div class="q-controls">
                    <button class="iconbtn" onclick={()=>{items[i].quantity++}}>add</button>
                    <button class="iconbtn" onclick={()=>{items[i].quantity--}}>remove</button>
                </div>
                <div class="divider"></div>
                <div class="price">${(item.price*item.quantity).toFixed(2)}</div>
            </div>
        {/each}
    </div>
    <div class="row">
        <strong>Subtotal</strong>
        <div class="divider"></div>
        <div class="price">${subtotal.toFixed(2)}</div>
    </div>
    <div class="row">
        <strong>Tax</strong>
        <div class="divider"></div>
        <div class="price">${tax.toFixed(2)}</div>
    </div>
    <div class="row total">
        <strong>Total</strong>
        <div class="divider"></div>
        <div class="price">${total.toFixed(2)}</div>
    </div>
    <div class="row actions">
        <button class="cancel" onclick={clearCart}>Cancel Order</button>
        <button class="checkout">Checkout</button>
    </div>
</div>
{/if}

<div class="contain">
    <button onclick={toggleReceipt}>
        Cart
    </button>
    <span class="cart-size">{cartSize}</span>
</div>

<style lang="scss">

    .actions {
        .checkout {
            background-color: var(--color-background);
            color: var(--color-accent);
            outline-color: var(--color-background);
        }
        
        .cancel {
            outline-color: var(--color-background);
        }

        button {
            flex-grow: 1;
            border-radius: 1rem;
        }
    }
    
    .iconbtn {
        outline: none;
        // background-color: red;
        border-radius: 0;
        padding: 0;
        width: fit-content;
        height: fit-content;
        img {
            height: 1em;
        }
    }

    .row {
        display: flex;
        justify-content: space-between;
        align-items: center;
        gap: 1rem;
        min-width: 100%;
        &.total * {
            font-size: 1.5rem;
        }
        span {
            white-space: nowrap;
        }
    }

    .q-controls {
        display: flex;
        gap: .25rem;
    }

    .divider {
        height: 2px;
        background-color: var(--color-accent-light);
        flex-grow: 1;
        min-width: 1rem;
    }

    h1 {
        font-family: var(--accent-font-family);
        font-weight: normal;
        font-style: italic;
    }

    .contain {
        position: relative;
    }

    .receipt {
        display: flex;
        flex-direction: column;
        padding: 2rem;
        border-radius: 3rem;
        position: absolute;
        right: 0;
        bottom: 5rem;
        gap: 1rem;
        min-width: 30rem;
        * {
            color: var(--color-background);
        }
        background-color: var(--color-accent);
        width: max-content;
        box-shadow: 0 0 2rem #00000077;
    }
    
    .items {
        display: flex;
        flex-direction: column;
        scrollbar-color: var(--color-accent-light) var(--color-accent);
        gap: 1.5rem;
        padding-right: .5rem;
        overflow-y: auto;
        max-height: 15rem;
        width: max-content;
    }

    button {
        display: flex;
        justify-content: center;
        align-items: center;
        transition-property: padding, outline-offset;
        padding: .5rem .5rem;
        border-radius: 5rem;
        width: 4rem;
        height: 4rem;
    }

    .cart-size {
        position: absolute;
        bottom: -2px;
        left: -.5rem;
        color: var(--color-background);
        background-color: var(--color-accent);
        border-radius: 5rem;
        width: 1.75rem;
        height: 1.75rem;
        display: block;
        display: flex;
        justify-content: center;
        align-items: center;
        border: 2px solid var(--color-background);
    }
</style>