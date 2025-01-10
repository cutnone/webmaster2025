<svelte:head>
    <title>Menu</title>
</svelte:head>

<script lang="ts">
	import ButtonSelector from '$lib/ButtonSelector.svelte';
	import Card from '$lib/Card.svelte';
	import Cart from '$lib/Cart.svelte';

	const items = [
		{
            id: 0,
			name: 'Cream of Mushroom',
			addons: ['Sourdough'],
			imageUrl: '/enoki/cream-of-mushroom.jpg',
			sizes: [
				{
					name: 'Cup',
					price: 5.99
				},
				{
					name: 'Bowl',
					price: 9.99
				}
			]
		},
		{
            id: 1,
			name: 'Thai Red Noodle',
			addons: ['Sourdough'],
			imageUrl: '/enoki/thai-red-noodle.jpg',
			sizes: [
				{
					name: 'Cup',
					price: 6.99
				},
				{
					name: 'Bowl',
					price: 10.99
				}
			]
		},
		{
            id: 2,
			name: 'Thai Green Noodle',
			addons: ['Sourdough'],
			imageUrl: '/enoki/thai-green-noodle.jpg',
			sizes: [
				{
					name: 'Cup',
					price: 6.99
				},
				{
					name: 'Bowl',
					price: 10.99
				}
			]
		},
		{
            id: 3,
			name: 'Firecracker Ramen',
			addons: ['Sourdough'],
			imageUrl: '/enoki/firecracker-ramen.jpg',
			sizes: [
				{
					name: 'Cup',
					price: 7.99
				},
				{
					name: 'Bowl',
					price: 11.99
				}
			]
		},
		{
            id: 4,
			name: 'Miso Ramen',
			addons: ['Sourdough'],
			imageUrl: '/enoki/miso-ramen.jpg',
			sizes: [
				{
					name: 'Cup',
					price: 7.99
				},
				{
					name: 'Bowl',
					price: 11.99
				}
			]
		},
		{
            id: 5,
			name: 'Green Goddess Soup',
			addons: ['Sourdough'],
			imageUrl: '/enoki/green-goddess-soup.jpg',
			sizes: [
				{
					name: 'Cup',
					price: 5.99
				},
				{
					name: 'Bowl',
					price: 9.99
				}
			]
		},
		{
            id: 6,
			name: 'Green Goddess Salad',
			imageUrl: '/enoki/green-goddess-salad.jpg',
			addons: null,
			sizes: [
				{
					name: 'Small',
					price: 6.99
				},
				{
					name: 'Large',
					price: 10.99
				}
			]
		},
		{
            id: 7,
			name: 'Chickpea Caesar',
			imageUrl: '/enoki/caesar-salad.jpg',
			addons: null,
			sizes: [
				{
					name: 'Small',
					price: 6.99
				},
				{
					name: 'Large',
					price: 10.99
				}
			]
		},
		{
            id: 8,
			name: "Lion's Mane",
			imageUrl: '/enoki/lions-mane.jpg',
			addons: null,
			sizes: [
				{
					name: 'Small',
					price: 6.99
				},
				{
					name: 'Large',
					price: 10.99
				}
			]
		},
		{
            id: 9,
			name: 'Dumpling Noodle',
			imageUrl: '/enoki/dumpling-noodle.jpg',
			addons: null,
			sizes: [
				{
					name: 'Small',
					price: 7.99
				},
				{
					name: 'Large',
					price: 11.99
				}
			]
		},
		{
            id: 10,
			name: 'Peach Burrata',
			imageUrl: '/enoki/peach-burrata.jpg',
			addons: null,
			sizes: [
				{
					name: 'Small',
					price: 6.99
				},
				{
					name: 'Large',
					price: 10.99
				}
			]
		}
	];

    let cart: any[] = $state([]);

    function addItemToCart(data: any) {

        const item = items[data.id];

        const size = item.sizes[data.size];

        for (const i of cart) {
            if (i.id === data.id && i.size === size.name) {
                i.quantity++;
                return;
            }
        }

        cart.push({
            id: data.id,
            name: item.name,
            size: size.name,
            price: size.price,
            quantity: 1,
        })



    }

	const menu = [
		{
			name: 'soup',
			items: [0, 1, 2, 3, 4, 5]
		},
		{
			name: 'salad',
			items: [6, 7, 8, 9, 10]
		}
	];
</script>

<main>
	<h1>our menu</h1>
	{#each menu as section}
		<div class="menu-section">
			<h2>{section.name}</h2>
			{#each section.items as id}
				<Card
                    itemId={id}
					onItemAdded={addItemToCart}
					name={items[id].name}
					addons={items[id].addons ? '+ ' + items[id].addons.join(', ') : null}
					sizes={items[id].sizes}
					imageUrl={items[id].imageUrl}
				/>
			{/each}
		</div>
	{/each}
</main>

<div class="cart-container">
    <Cart bind:items={cart}/>
</div>

<style lang="scss">

    .cart-container {
        position: fixed;
        bottom: 5rem;
        right: 5rem;
    }

	h1,
	h2 {
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

	@media (max-width: 750px) {
		h2 {
			text-align: center;
			padding: 0;
		}

		.cart-container {
			width: 100vw;
			padding: 2rem;
			right: 0;
			bottom: 0;
		}
	}
</style>
