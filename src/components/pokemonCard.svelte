<script>
    import { fade } from 'svelte/transition'

    export let pokemon
</script>

<a
    class="my-2 p-6 bg-transparent text-gray-800 min-w-60
            text-center rounded-lg shadow-lg hover:shadow-xl 
            border border-opacity-20
            flex flex-col items-center"
    href={`/pokemon/${pokemon.id}`}
    transition:fade
>
    <img class="h-40 w-40" src={pokemon.image} alt={pokemon.name} />
    <h2 class="uppercase text-2xl">{pokemon.id}. {pokemon.name}</h2>
</a>
