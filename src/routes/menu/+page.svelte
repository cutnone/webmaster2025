<script>
	import Card from "$lib/Card.svelte";

</script>
<main>
    <h1>our menu</h1>
    <div class="menu-section">
        <h2>soup</h2>
        <Card name="cream of mushroom" addons="+ Sourdough" price="$9.99" imageUrl="https://unsplash.it/500"/>
        <Card name="thai red noodle" addons="+ Sourdough" price="$9.99" imageUrl="https://unsplash.it/500"/>
        <Card name="thai green noodle" addons="+ Sourdough" price="$9.99" imageUrl="https://unsplash.it/500"/>
        <Card name="firecracker ramen" addons="+ Sourdough" price="$9.99" imageUrl="https://unsplash.it/500"/>
        <Card name="miso ramen" addons="+ Sourdough" price="$9.99" imageUrl="https://unsplash.it/500"/>
        <Card name="green goddess" addons="+ Sourdough" price="$9.99" imageUrl="https://unsplash.it/500"/>
    </div>
    <div class="menu-section">
        <h2>salad</h2>
        <Card name="green goddess" price="$9.99" imageUrl="https://unsplash.it/500"/>
        <Card name="chickpea caesar" price="$9.99" imageUrl="https://unsplash.it/500"/>
        <Card name="lion's mane" price="$9.99" imageUrl="https://unsplash.it/500"/>
        <Card name="dumpling noodle" price="$9.99" imageUrl="https://unsplash.it/500"/>
        <Card name="peach burrata" price="$9.99" imageUrl="https://unsplash.it/500"/>
    </div>
</main>

<style lang="scss">
    h1, h2 {
        font-family: var(--accent-font-family);
        font-style: italic;
        font-weight: normal;
    }
    h1 {
        text-align: center;
        font-size: 4rem;
        margin-top: 1rem;
    }
    
    h2 {
        grid-column: 1 / -1;
        padding-left: 1rem;
        font-size: 3rem;
    }

    .menu-section {
        max-width: calc(4 * 30ch + 3 * 1rem + 4rem);
        width: 100%;
        padding: 1rem 2rem;
        margin: auto;
        display: grid;
        grid-template-columns: repeat(auto-fill, 30ch);
        flex-wrap: wrap;
        gap: 1rem;
        justify-content: center;
    }

    main {
        display: flex;
        flex-direction: column;
        gap: 1.5rem;
        padding: 1.5rem 0;
    }
</style>