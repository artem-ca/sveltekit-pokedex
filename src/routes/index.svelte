<script context="module">
    export async function load({ page }) {
        const url = `https://pokeapi.co/api/v2/pokemon?limit=100`
        const res = await fetch(url)
        const data = await res.json()
        const loadedPokemon = data.results.map((data, index) => {
            return {
                name: data.name,
                id: index + 1,
                image: `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${
                    index + 1
                }.png`,
            }
        })
        return { props: { pokemon: loadedPokemon } }
    }
</script>

<script>
    import PokemonCard from '../components/pokemonCard.svelte'

    export let pokemon

    let searchTerm = ''
    let filteredPokemon = []

    $: {
        if (searchTerm) {
            filteredPokemon = pokemon.filter((pokemon) =>
                pokemon.name
                    .toLowerCase()
                    .trim()
                    .includes(searchTerm.toLowerCase().trim())
            )
        } else {
            filteredPokemon = [...pokemon]
        }
    }
</script>

<svelte:head>
    <title>Svelte Kit Pokedex</title>
</svelte:head>

<h1 class="text-3xl text-center my-8 uppercase">Svelte Kit Pokedex</h1>

<input
    class="w-full text-xl p-3 outline-none bg-transparent
    border-2 border-t-0 border-r-0 border-l-0 border-opacity-30 border-gray-900"
    type="text"
    placeholder="Search pokemon"
    bind:value={searchTerm}
/>

<div class="py-4 my-5 flex flex-wrap justify-center gap-10">
    {#each filteredPokemon as pokemon}
        <PokemonCard {pokemon} />
    {/each}
</div>

<style>
</style>
