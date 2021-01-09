<script>

    export let name
    export let picture
    
</script>

<div class="carte">
    <p class="nom">{name}</p>
    <img src="{picture}" alt="pokémon">
    
</div>


<style>

    .carte {
        width: 300px;
        height: 200px;
        background-color: #228b223a;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        margin: 5px;
    }

    .carte img{
        width: 100px;
    }

    .carte p {
        font-size: 25px;
    }

</style>