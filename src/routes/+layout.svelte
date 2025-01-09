
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
        nav
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
        justify-content: center;
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


</style>