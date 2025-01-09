
<div class="hero">
    <img class="himg" src="/hero-soup.jpg" alt="">
    <img class="mushrooms" src="/mushrooms-white.svg" alt="">
    <h1>come on in</h1>
    <h2>we have mushroom for everyone</h2>
</div>
<div class="cta">
    <button>start an order</button>
    <span>open 11 a.m. - 9 p.m. | tue thru sun</span>
    <img class="mushrooms-2" src="/mushrooms-green.svg" alt="">
</div>
<div class="blurb">
    <figure>
        <img src="https://unsplash.it/500" alt="">
        <div class="overlay"></div>
        <figcaption>miso ramen</figcaption>
    </figure>
    <div class="content">
        <img src="https://unsplash.it/500" alt="" class="bg">
        <h2>enoki is a vegetarian restaurant in the Philadelphia area harnessing the unique flavors and textures of mushrooms to create familiar yet surprising dishes.</h2>
        <p>Our mushrooms are sourced from Kennett Square, a local town in Chester County, PA. Kennett Square is the renowned “Mushroom Capital of the World”, producing 50% of the world’s mushrooms.</p>
        <a href="/about">Learn More</a>
    </div>
    <figure>
        <img src="https://unsplash.it/500" alt="">
        <div class="overlay"></div>
        <figcaption>green goddess salad</figcaption>
    </figure>
</div>
<style lang="scss">

    .hero {
        position: relative;
        font-family: var(--accent-font-family);
        padding-bottom: 3.5rem;
        img.himg {
            width: 100%;
            height: 35rem;
            filter: brightness(.7) contrast(.8);
        }
        .mushrooms {
            position: absolute;
            bottom: 0;
            left: 50px;
        }

        h1 {
            font-size: 10rem;
            color: var(--color-background);
            position: absolute;
            bottom: .2rem;
            right: 5rem;
        }
        
        h2 {
            font-size: 3rem;
            color: var(--color-accent);
            position: absolute;
            bottom: 0;
            right: 2rem;
        }
    }

    figure {
        position: relative;
        // display: block;
        img {
            width: 100%;
            height: 100%;
        }
        .overlay {
            width: 100%;
            height: 5rem;
            background-color: black;
            position: absolute;
            bottom: 0;
            background: linear-gradient(to top, #000000bb, transparent);
        }
        figcaption {
            position: absolute;
            bottom: 0;
            width: 100%;
            padding: 1rem;
            font-family: var(--accent-font-family);
            color: var(--color-background);
        }
    }

    .cta {
        position: relative;
        font-family: var(--accent-font-family);
        button {
            font-family: var(--accent-font-family);
            font-size: 2rem;
            padding: 1.5rem 3rem;
            border-radius: 1rem;
        }
        span {
            color: var(--color-accent);
            font-size: 1.5rem;
        }
        display: flex;
        gap: 2em;
        align-items: center;
        padding: 0 3.5rem 3.5rem 3.5rem;

        .mushrooms-2 {
            position: absolute;
            right: 3rem;
            bottom: -1rem;
            height: 10rem;
            opacity: .5;
        }
    }

    .blurb {
        display: flex;
        height: 30rem;
        .content {
            position: relative;
            display: grid;
            // place-items: center;
            justify-content: center;
            align-content: center;
            align-items: center;
            gap: 2rem;
            padding: 4rem;
            h2 {
                font-family: var(--accent-font-family);
            }
            * {
                color: var(--color-background);
                max-width: 35rem;
            }
            a {
                color: var(--color-accent-light);
            }
            img {
                position: absolute;
                inset: 0;
                min-width: 100%;
                height: 100%;
                z-index: -1;
                filter: brightness(.3);
            }
            flex-grow: 2;
        }
        figure {
            flex-grow: 1;
            flex-basis: 20rem;
        }
    }
    img {
        object-fit: cover;
        display: block;
    }
</style>