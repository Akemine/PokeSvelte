<script>

import BarreDeRecherche from './BarreDeRecherche.svelte'
import Carte from './Carte.svelte'
import {v4 as uuidv4} from 'uuid'

let allPokemon = []
let tableauFin = []

function fetchPokemonBase(){
    fetch('https://pokeapi.co/api/v2/pokemon?limit=151')
    .then(reponse => reponse.json()
    .then(function(allPokemon){
        allPokemon.results.forEach(function(pokemon){
            fetchPokemonComplet(pokemon)
        })
    }))
}

function fetchPokemonComplet(pokemon){

        let objPokemonFull = {}
        let url = pokemon.url
        let name = pokemon.name
        fetch(url)
        .then(reponse => reponse.json())
        .then(function(pokeData){
            objPokemonFull.picture = pokeData.sprites.back_default

            fetch(`https://pokeapi.co/api/v2/pokemon-species/${name}`)
            .then(reponse => reponse.json())
            .then(function(pokeData){
                objPokemonFull.name = pokeData.names[4].name

                allPokemon = [...allPokemon, objPokemonFull]
            })
            .then(() => {
                tableauFin = allPokemon.slice(0, 10)
            })
        })
}

fetchPokemonBase()


function goRecherche(e){
    let contenuRecherche = e.detail.txt
    tableauFin = allPokemon.filter(el => el.name.includes(contenuRecherche))
}

function goRechercheAll(){
    let contenuRecherche = ""
    tableauFin = allPokemon.filter(el => el.name.includes(contenuRecherche))
}




</script>


    <BarreDeRecherche on:recherche-pokemon={goRecherche} on:rechercheAll-pokemon={goRechercheAll}/>

    <div class="contenu">

        {#each tableauFin as pokemon (uuidv4())}
            <Carte name={pokemon.name} picture={pokemon.picture}/>
        {/each}
        
    </div>

<style>

    .contenu{
        max-width: 1400px;
        width: 95%;
        padding: 0 50px;
        margin: 0 auto;
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
    }

</style>