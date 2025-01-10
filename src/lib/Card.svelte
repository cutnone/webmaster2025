<script lang="ts">
	import { expoOut } from "svelte/easing";
	import { slide } from "svelte/transition";
	import ButtonSelector from "./ButtonSelector.svelte";

    const { itemId, name, addons = null, sizes, imageUrl, onItemAdded} = $props();

    let adding = $state(false);

    let activeSize = $state(0)

    function addClick() {
        if (!adding) {
            adding = true;
        } else {
            onItemAdded({
                id: itemId,
                size: activeSize,
            })
            stopAdding()
        }
    }

    function stopAdding() {
        adding = false;
        activeSize = 0;
    }
</script>

<div class="card">
    <img src={imageUrl} alt="">
    <div class="text-cluster">
        {#if addons}
            <h3>{name}</h3>
            <div class="row">
                <span class="addons">{addons}</span>
                <div class="price">{sizes[activeSize].price}</div>
            </div>
            {:else}
            <div class="row">
                <h3>{name}</h3>
                <div class="price">{sizes[activeSize].price}</div>
            </div>
        {/if}
    </div>
    <div class="row btnrow" class:showing={adding}>
        <button onclick={stopAdding} class="iconbtn close">
            <img class="icon" src="/enoki/icon-cross-green.svg" alt="">
        </button>
        <ButtonSelector options={sizes.map((v: any)=>v.name)} bind:selected={activeSize}/>
        <button class="iconbtn close">
            <img class="icon" src="/enoki/icon-check.svg" alt="">
        </button>
    </div>
    <button class="addbtn" onclick={addClick} class:iconbtn={adding}>
        {#if adding}
            <img transition:slide={{axis: "x", duration: 300, easing: expoOut}} class="icon" src="/enoki/icon-check.svg" alt="">
        {:else}
            <span transition:slide={{axis: "x", duration: 300, easing: expoOut}}>Add to Order</span>
        {/if}
    </button>
</div>

<style lang="scss">

    .addbtn {
        position: absolute;
        bottom: 1rem;
        right: 1rem;
    }

    .iconbtn {
        &:hover {
            outline-offset: .125em;
        }
        &:active {
            outline-offset: .0625em;
        }
    }

    .btnrow {
        transition-property: scale, opacity;
        transform-origin: 0;
        &:not(.showing) {
            opacity: 0;
            scale: 0.5;
        }
    }


    .icon {
        height: 1.2em;
        width: 1.2em;
        vertical-align: middle;
    }

    .close {
        background-color: var(--color-background);
    }
    .card {
        position: relative;
        border-radius: 2rem;
        padding: 1rem;
        border: .25rem solid var(--color-background-alt);
        width: 30ch;
        background-color: var(--color-background);
        box-shadow: 0 0 2rem #00000077;
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
        object-fit: cover;
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

    .btnrow {
        gap: .25rem;
    }

    .text-cluster {
        display: flex;
        flex-direction: column;
        gap: .25rem;
        padding: .5rem;
    }

    button {
        display: flex;
        justify-content: center;
        align-items: center;
        transition-property: padding, outline-offset;
        // flex-grow: 1;
        padding: .5rem .5rem;
        border-radius: 1rem;
        span {
            color: var(--color-background);
            white-space: nowrap;
            width: calc(29ch);
        }
    }

</style>