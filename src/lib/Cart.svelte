<script lang="ts">
	import { onMount } from "svelte";
	import { expoOut } from "svelte/easing";
	import { scale, slide } from "svelte/transition";


    const {items = $bindable([])} = $props();

    let cartSize = $derived(items.reduce((acc, v)=>acc+(v.quantity), 0))

    let subtotal = $derived(items.reduce((acc, v)=>acc+(v.price*v.quantity), 0))
    let tax = $derived(subtotal * .06);
    let total = $derived(subtotal + tax);

    let receiptOpen = $state(false);

    let confirmationOpen = $state(false);

    onMount(()=>{
        console.log("getting ls");
        
        let newItems = JSON.parse(localStorage.getItem("cart") ?? "[]");
        items.length = 0;
        items.push(...newItems)
    })
    
    $effect(()=>{
        localStorage.setItem("cart", JSON.stringify(items));
    })

    $effect(()=>{
        if (items.length === 0 && !confirmationOpen) {
            receiptOpen = false;
        }
    })
    
    $effect(()=>{
        if (items.length === 1) {
            receiptOpen = true;
        }
    })

    function toggleReceipt() {
        if (items.length === 0) {
            closeReceipt()
            return;
        }
        if (!receiptOpen) {
            receiptOpen = true;
            return;
        } 
        closeReceipt();
    }

    function closeReceipt() {
        confirmationOpen = false;
        receiptOpen = false;
    }

    function clearCart() {
        // items.splice(0, items.length);
        items.length = 0;
    }

    function removeItem(i: number) {
        items.splice(i, 1)
    }

    function decrease(i: number) {
        let item = items[i];
        if (item.quantity > 1) item.quantity--;
        else removeItem(i);
    }

    function increase(i: number) {
        let item = items[i];
        item.quantity++;
    }

    function closeConfirmation() {
        confirmationOpen = false;
    }

    function checkout() {
        clearCart();
        confirmationOpen = true;
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
                <button class="iconbtn" onclick={()=>removeItem(i)}><img src="/enoki/icon-cross.svg" alt=""></button>
                <span>{item.name} ({item.size}) x{item.quantity}</span>
                <div class="q-controls">
                    <button class="iconbtn" onclick={()=>increase(i)}><img src="/enoki/icon-plus.svg" alt=""></button>
                    <button class="iconbtn" onclick={()=>decrease(i)}><img src="/enoki/icon-minus.svg" alt=""></button>
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
        <button class="checkout" onclick={checkout}>Checkout</button>
    </div>
    {#if confirmationOpen}
        <div transition:scale={{easing: expoOut, duration: 300,}} class="confirmation">
            <h3>order placed.</h3>
            <p>Thank you!</p>
            <button onclick={closeConfirmation}>Go Back</button>
        </div>
    {/if}
</div>
{/if}

<div class="contain">
    <button class="cart" onclick={toggleReceipt}>
        <img src="/enoki/icon-shopping-basket.svg" alt="">
        <span class="label">My Cart ({cartSize} items)</span>
    </button>
    <span class="cart-size">{cartSize}</span>
</div>

<style lang="scss">

    .confirmation {
        position: absolute;
        inset: 0;
        background-color: var(--color-accent);
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        border-radius: 3rem;
        width: 100%;
        height: 100%;

        button {
            font-size: 1rem;
            background-color: var(--color-background);
            outline-color: var(--color-background);
            color: var(--color-accent);
            width: max-content;
            padding: .5rem 1rem;
            height: fit-content;
        }
        gap: 1rem;
    }

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
            font-size: 1rem;
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

    .cart {
        img {
            height: 2rem;
        }

        .label {
            display: none;
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
        gap: .5rem;
    }

    .divider {
        height: 2px;
        background-color: var(--color-accent-light);
        flex-grow: 1;
        min-width: 1rem;
    }

    h1, h3 {
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
        // width: max(max-content, 100%);
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
        left: -.7rem;
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

    @media (max-width: 750px) {
        .contain {
            width: 100%;

            .cart {
                width: 100%;
                font-size: 1rem;
                display: flex;
                gap: 1rem;
                justify-content: center;
                * {
                    color: var(--color-background);
                }

                .label {
                    display: inline;
                }
            }

            .cart-size {
                display: none;
            }
        }

        .receipt {
            position: static;
            width: 100%;
            max-width: 100%;
            min-width: 100%;
            margin-bottom: 2rem;
            .row {
                flex-wrap: wrap;
            }
            .items {
                max-height: 10rem;
            }
        }
    }
</style>