<script>
    
import {createEventDispatcher} from 'svelte'

const dispatch = createEventDispatcher()

let recherche = ""
let rechercheAll = ""

function rechercheFunc(){
    dispatch('recherche-pokemon', {txt: recherche})
    // recherche = "" Réactiver cette ligne pour que la recherche se réinitialise
}

function rechercheFuncAll(){
    dispatch('rechercheAll-pokemon', {txt: rechercheAll})
     recherche = "" 
}

</script>


<form class="form-recherche" on:submit|preventDefault={rechercheFunc}>
    <label for="recherche">Chercher un Pokémon</label>
    <input bind:value={recherche} type="text" id="recherche" placeholder="Rechercher un Pokémon">
    <button type="submit">Recherche</button>
</form>

<form class="form-rechercheAll" on:submit|preventDefault={rechercheFuncAll}>
    <input bind:value={rechercheAll} type="hidden" id="rechercheAll" placeholder="Rechercher un Pokémon">
    <button class="rechercheAll" type="submit">Voir toute la liste</button>
</form>


<style>

    .form-recherche{
        margin: 100px auto 0px auto;
        max-width: 1100px;
        width:100%;
        padding: 0 50px;
        /* display: flex; */
        align-content: center;
        flex-direction: column;
    }

    .form-rechercheAll{
        margin: 0px auto 50px auto;
        max-width: 1100px;
        width:100%;
        padding: 0 50px;
        /* display: flex; */
        align-content: center;
        flex-direction: column;
    }

    .form-recherche input, .form-recherche label {
        max-width: 1100px;
        width:100%;
    }

    .form-recherche label{
        font-size: 25px;
        border: none;
        padding: 10px 0;
    }

    .form-recherche input{
        font-size: 20px;
        padding: 20px;
        background-color: #acddac;
    }

    form button {
        padding: 15px 30px;
        background: forestgreen;
        color: white;
        border: none;
        outline: none;
        cursor: pointer;
        margin-top: 5px;
        font-size: 18px;
        margin-right: auto;
    }

    button:hover{
        background: green;
    }

    button, .rechercheAll {
        background-color:  rgb(80, 192, 80);
    }
</style>

