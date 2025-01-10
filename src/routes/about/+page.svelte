<svelte:head>
    <title>About Us</title>
</svelte:head>

<h1>about us</h1>
<article>
    <div class="sbs">
        <div class="col">
            <h2>meet our founder- he's a fun-gi!</h2>
            <span>Chef Akari Ito has always had an affinity towards the culinary arts. Despite Ito’s passion for food and unique flavors, his passion for the environment has led him down a new path as a vegetarian. Despite giving up meat, Ito has utilized the unique properties of mushrooms and other plants to create satiating and tasty meals. </span>
            <span>At Enoki, we believe that eating plant-based food can be delicious and flavorful. We hope to provide a unique experience with our cozy restaurant space, vibrant salads, and hearty soups. Whether you are strictly vegetarian or just looking to try new flavors, Enoki has something to offer.</span>
        </div>
        <img src="/enoki/founder.jpg" alt="">
    </div>
    <h2>why mushrooms?</h2>
    <p>
        There are many reasons!
    </p>
    <h3>nutrition</h3>
    <ul>
        <li>They are a good source of vitamins B & D.</li>
        <li>There are many polysaccharides in mushrooms which are prebiotics, and can improve overall digestion.</li>
        <li>The amino acid glutamate can be found in many mushrooms, creating vibrant umami flavors.</li>
    </ul>
    <h3>sustainability</h3>
    <ul>
        <li>Mushrooms produce high yields in small spaces, and about 891 million pounds of mushrooms can be grown in a year, given 1 square mile of space.</li>
        <li>Mushrooms mature in about 6-10 weeks, allowing for multiple crop yields in the same year.</li>
        <li>Mushrooms are decomposers, and can therefore be grown using agricultural waste from other types of farms.</li>
    </ul>
    <img src="/enoki/mushroom-collage.jpg" alt="">
    <h2>how are our mushrooms grown?</h2>
    <p>Our mushrooms are a local product from Kennett Square, a town in Chester County, PA. This small town is known for its large mushroom farms, producing 50% of the world’s mushrooms.</p>
    <p>Historically, horse manure from nearby cities was mixed with hay and cocoa shells from Hershey chocolate factory. This mix of ingredients is the ideal formula for growing mushroom spores. Spores are placed inside the manure and are left to grow in moderated buildings with the proper amount of water, carbon, and heat. Once mature, these mushrooms are shipped directly to our restuarant.</p>
</article>

<style lang="scss">
    h1, h2, h3 {
        font-family: var(--accent-font-family);
        font-style: italic;
    }

    h2 {
        font-size: 1.75rem;
    }

    h1 {
        text-align: center;
		font-size: 4rem;
		margin-top: 1rem;
        font-weight: normal;
    }
    article {
        max-width: 75ch;
        margin: auto;
        padding: 2rem;
        display: flex;
        flex-direction: column;
        gap: 1rem;
    }
    img {
        border-radius: 1rem;
        object-fit: cover;
        // min-width: 10rem;
        min-width: 20rem;
        max-width: 100%;
        max-height: 30rem;
    }

    .col {
        display: flex;
        flex-direction: column;
        gap: 1rem;
    }

    .sbs {
        display: flex;
        gap: 1rem;
    }

    @media (max-width: 650px) {
        .sbs {
            flex-direction: column;
            img {
                min-width: 0;
            }
        }

        img {
            max-width: 100%;

        }
    }

</style>