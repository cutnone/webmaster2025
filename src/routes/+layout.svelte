
<svelte:head>
    <title>Enoki</title>
</svelte:head>

<script lang="ts">
    import '$lib/styles.scss'
	import { onMount } from 'svelte';
	import { expoOut } from 'svelte/easing';
	import { slide } from 'svelte/transition';

    let navOpen = $state(false);

    function toggleNav() {
        navOpen = !navOpen;
    }

    let mobileMq;

    onMount(()=>{
        mobileMq = matchMedia("(max-width: 750px)");
        mobileMq.addEventListener("change", (e)=>{
            navOpen = navOpen && e.matches;
        })
    })



	let { children } = $props();
</script>


<header>
    <a href="/"><img src="/logowhite.svg" alt="" class="logo"></a>
    <nav>
        <a href="/">home</a>
        <a href="/about">about us</a>
        <a href="/menu">menu</a>
        <a href="/references">references</a>
    </nav>
    <div class="user">
        <span>hi, guest!</span>
        <img src="" alt="" class="pfp">
    </div>
    <button class="open-nav" onclick={toggleNav}>
        {#if navOpen}
            <img 
                in:slide={{easing: expoOut, duration: 300}} 
                out:slide={{easing: expoOut, duration: 300}} 
            src="/icon-cross.svg" alt="">
        {:else}
            <img 
                in:slide={{easing: expoOut, duration: 300}} 
                out:slide={{easing: expoOut, duration: 300}}  
            src="/icon-burger.svg" alt="">
        {/if}
    </button>
</header>

{#if navOpen}
<div class="mobile-nav" transition:slide={{axis: "y", duration: 1000, easing: expoOut}}>
    <a href="/" onclick={toggleNav}>home</a>
    <a href="/about" onclick={toggleNav}>about us</a>
    <a href="/menu" onclick={toggleNav}>menu</a>
    <a href="/references" onclick={toggleNav}>references</a>
</div>
{/if}

{@render children()}

<footer>
    <div class="contact">
        <h2>contact us</h2>
        <span><a href="mailto:contact@enoki.com">contact@enoki.com</a> (not a real email)</span>
        <span><a href="tel:+12676804779">+1 (267) 680-4779</a> (not real a phone number)</span>
        <span><a href="https://maps.app.goo.gl/YB4oz79MZ4xiWmcm7">123 Melody Drive, Springfield PA, 19064</a> (not a real place)</span>

    </div>
    <!-- <nav>
        <a href="/">Home</a>
        <a href="/about">About Us</a>
        <a href="/menu">Menu</a>
        <a href="/references">References</a>
    </nav> -->
    <p>
        © 2025 Enoki Restaurant. All rights reserved.
    </p>
</footer>


<style lang='scss'>

    .mobile-nav {
        position: fixed;
        inset: 0;
        width: 100vw;
        height: 100dvh;
        background-color: var(--color-accent);
        padding: 2rem;
        padding-top: 8rem;
        display: flex;
        flex-direction: column;
        z-index: 1;
        gap: 2rem;
        a {
            font-weight: normal;
            font-family: var(--accent-font-family);
            font-size: 3rem;
            color: var(--color-background);
        }
    }

    .open-nav {
        display: none;
        background-color: transparent;
        outline: none;
        padding: 0;
        border-radius: 0;

        img {
            height: 2em;
        }
    }

    footer, header {
        * {
            color: var(--color-background);
        }

        background-color: var(--color-accent);
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 1rem;
    }

    footer {
        justify-content: space-between;
        align-items: center;
        
        .contact {
            display: flex;
            gap: 1rem;
            align-items: center;
            a {
                text-decoration: underline;
            }
            h2 {
                font-weight: normal;
                font-style: italic;
                font-family: var(--accent-font-family);
            }
        }
    }

    header {
        font-family: var(--accent-font-family);
        font-size: 1.2rem;
        position: sticky;
        top: 0;
        z-index: 2;
    }

    nav {
        display: flex;
        gap: 2ch;
    }

    .logo {
        height: 2rem;
    }

    @media (max-width: 750px) {
        header nav, .user {
            display: none;
        }

        .open-nav {
            display: block;
        }
    }

    @media (max-width: 1625px) {

        footer {
            align-items: end;
            .contact {
                flex-direction: column;
                gap: .5rem;
                align-items: start;
            }
        }
    }

    @media (max-width: 850px) {

        footer {
            flex-direction: column;
            justify-content: start;
            align-items: start;
            gap: 1rem;
        }
    }


</style>