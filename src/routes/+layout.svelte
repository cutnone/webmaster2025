
<script lang="ts">
    import '$lib/styles.scss'

	let { children } = $props();
</script>


<header>
    <a href="/"><img src="/logowhite.svg" alt="" class="logo"></a>
    <nav>
        <a href="">About Us</a>
        <a href="">Menu</a>
        <a href="">References</a>
    </nav>
    <div class="user">
        <span>hi, guest!</span>
        <img src="" alt="" class="pfp">
    </div>
</header>

{@render children()}

<footer>
    <nav>
        <a href="">Home</a>
        <a href="">About Us</a>
        <a href="">Menu</a>
        <a href="">References</a>
    </nav>
    <p>
        © 2025 Enoki Restaurant. All rights reserved.
    </p>
</footer>


<style lang='scss'>

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

    header {
        font-family: var(--accent-font-family);
        font-size: 1.2rem;
    }

    nav {
        display: flex;
        gap: 2ch;
    }

    .logo {
        height: 2rem;
    }


</style>