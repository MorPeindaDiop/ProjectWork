<head>
    
    <style>
        body{background-color:black;}
        /*----  Main Style  ----*/
        #cards_landscape_wrap-2 {
            text-align: center;
            background: rgb(51, 52, 51);
            border-radius: 2%;
        }

        h2{
            padding-top:2%;
            color:white;
        }
    </style>
</head>

<script>
    import {link} from 'svelte-spa-router';
    import { location} from 'svelte-spa-router'
    import { onMount } from 'svelte';
    import Api from '../Api.js';
    export const idUrl = $location
    let arrayUrl=idUrl.split('/');
    let modelli = [];
    let modelli2 = [];
    let idMarca;

onMount(async () => {
    const response = await Api.get('/modelli/findAll')
    let marche = await Api.get('/marche/findAll')

    for (let marca of marche.result) {
        if (marca.marca == arrayUrl[arrayUrl.length -1]) {
        idMarca=marca.id_Marca;
        }
    }
    for (let modello of response.result) {
        if (modello.id_Marca == idMarca) {
            modelli.push(modello);
            stampo()
        }

    }
//console.log(modelli);

});
function stampo() {
    modelli2 = modelli;
}
  </script>




<!-- Topic Cards -->
<!-- <p style="color:white">a {modelli2.lenght}</p> -->
<!-- {#if modelli.lenght == undefined} -->
{#await onMount}

<!-- promise is pending -->
<p>waiting for the promise to resolve...</p>
{:then stampo}
<!-- <p style="color:white">b {modelli2.length}</p> -->
<div id="cards_landscape_wrap-2">
    <h2>Seleziona la motorizzazione</h2>
    <div class="container">
        <div class="row">
            {#each modelli2 as modello}
            <div class="col-xs-12 col-sm-6 col-md-3 col-lg-3">
                <a href="{idUrl}/{modello.modello}" use:link>
                    <div class="card-flyer">
                        <div class="text-box">
                            <div class="image-box">
                                <img
                                    src="{modello.src}"
                                    alt=""
                                />
                            </div>
                            <div class="text-container">
                                <h6>{modello.modello}</h6>
                            </div>
                        </div>
                    </div>
                </a>
            </div>
            {/each}
            
        </div>
    </div>
</div>
<!-- {/if} -->
{/await}