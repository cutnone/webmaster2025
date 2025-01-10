<svelte:head>
    <title>References</title>
</svelte:head>

<article>
    <img src="/mushrooms-black.svg" alt="">
    <section>
        <h2>references</h2>
        <p class="links">
            <a href="https://drive.google.com/file/d/1A7JB05rW6TTA9tqngZyU39zHQC1VUFdi/view?usp=sharing">Copyright Checklist</a>,
            <a href="https://drive.google.com/file/d/1WQBUuUP9XL8mdw20fuoLAD1VEh0nQ-lb/view?usp=sharing">Plan of Work Log</a>,
            <a href="">Works Cited</a>
        </p>
        <p>Built with <a href="https://svelte.dev/">SvelteKit (Svelte 5)</a>. We made the theme from scratch.</p>
        <p><em>Thank you for taking the time to judge our site!</em></p>
    </section>
</article>

<style lang="scss">
    h1, h2, h3 {
        font-family: var(--accent-font-family);
        font-style: italic;
    }

    article {
        width: 100vw;
        height: calc(100dvh - 4rem);
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 2rem;
        padding: 2rem;
    }
    
    section {
        
        display: flex;
        flex-direction: column;
        gap: .5rem;
    }
    
    a {
        color: var(--color-accent);
    }

    img {
        height: 10rem;
        translate: .3rem 0;
        scale: -1 1;
    }

</style>