<head>

    <style>
        body{background-color:black;}
        /*----  Main Style  ----*/
        #cards_landscape_wrap-2 {
            text-align: center;
            background: rgb(51, 52, 51);
           -webkit-border-radius: 20px;
           -moz-border-radius: 20px;
           border-radius:20px;
           padding-bottom: 3%;
        }

        h2{
            padding-top:2%;
            color:white;
        }
        p{color:white}
        img{
            padding-top:2%;
            padding-bottom:2%;
            width:40%;
            height:40%;
        }
        .table{
            
            background-color:white;
            width:80%;
            margin:0 auto;
            -webkit-border-radius: 15px;
           
        }
        button {background-color: #008CBA;} /* Blue */
        
    </style>
</head>

<script>
    import {link} from 'svelte-spa-router';
    import { location} from 'svelte-spa-router'
    import { onMount } from 'svelte';
    import Api from '../Api.js';
    export let idUrl = $location
    idUrl = idUrl.replace(/%20/g,' ');
    console.log(idUrl)
    let arrayUrl=idUrl.split('/');
    let motorizzazioni = [];
    let motorizzazioni2 = [];
    let idModello;
    let modelloProva;

onMount(async () => {
    let response = await Api.get('/motorizzazioni/findAll')
    let modelli = await Api.get('/modelli/findAll')

    for (let modello of modelli.result) {
        if (modello.modello == arrayUrl[arrayUrl.length -1]) {
            idModello=modello.id_Modello;
            modelloProva=modello
        }
    }
    for (let motorizzazione of response.result) {
        if (motorizzazione.id_Modello == idModello) {
            motorizzazioni.push(motorizzazione);
            stampo()
        }

    }
//console.log(modelli);

});
function stampo() {
    motorizzazioni2 = motorizzazioni;
    console.log(motorizzazioni2)
}
  </script>

<div id="cards_landscape_wrap-2">
{#if modelloProva != undefined}
<img src="{modelloProva.src}" alt="">
<table class="table table-hover">
    <thead>
      <tr>
        <th scope="col">Motore</th>
        <th scope="col">Alimentazione</th>
        <th scope="col">Cambio</th>
        <th scope="col">Consumo</th>
      </tr>
    </thead>
    <tbody>
        {#each motorizzazioni2 as motorizzazione2}
      <tr>
        <td>{motorizzazione2.motore}</td>
        <td>{motorizzazione2.alimentazione}</td>
        <td>{motorizzazione2.cambio}</td>
        <td>{motorizzazione2.consumo}</td>
        <td> <a href=""> <button>SELEZIONA</button> </a></td>
      </tr>
      {/each}
    </tbody>
  </table>
<!-- <p>{motorizzazione2.descrizione}</p> -->

{/if}
</div>