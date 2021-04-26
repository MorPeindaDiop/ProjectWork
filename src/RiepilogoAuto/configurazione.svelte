<script>
    import { link } from "svelte-spa-router";
    import { location } from "svelte-spa-router";
    import { onMount } from "svelte";
    import Api from "../Api.js";
    export let idUrl = $location;
    idUrl = idUrl.replace(/%20/g, " ");
    console.log(idUrl);
    let arrayUrl = idUrl.split("/");
    let colori = [];
    let colori2 = [];
    let idModello;
    let RiepilogoModello;
    let RiepilogoMarca;
    let srcSelected = "";
    let RiepilogoColore;
    let RiepilogoMotorizzazione;
    let RiepilogoAllestimento;
    let srcFinale="";

    onMount(async () => {
        let response = await Api.get("/configurazione/findAll");
        let modelli = await Api.get("/modelli/findAll");
        let marche = await Api.get("/marche/findAll");
        let colori = await Api.get("/colore/findAll");
        let motorizzazioni = await Api.get("/motorizzazioni/findAll");
        let allestimenti = await Api.get("/allestimento/findAll");

        

        for (let marca of marche.result) {
            if (marca.marca == arrayUrl[2]) {
                RiepilogoMarca = marca.marca;
            }
        }

        for (let modello of modelli.result) {
            if (modello.modello == arrayUrl[3]) {
                idModello = modello.id_Modello;
                RiepilogoModello=modello.modello
            }
        }

        for (let motorizzazione of motorizzazioni.result) {
            if (motorizzazione.id_Motorizzazione == arrayUrl[4]) {
                RiepilogoMotorizzazione = motorizzazione.motore;
            }
        }

        for (let allestimento of allestimenti.result) {
            if (allestimento.descrizione == arrayUrl[5]) {
                RiepilogoAllestimento = allestimento.descrizione;
            }
        }

        for (let colore of colori.result) {
           
                if(idModello==colore.id_Modello){
                    if (colore.descrizione == arrayUrl[6]) {
                
                 RiepilogoColore = colore.descrizione;
                srcFinale=colore.src;
                }
                
                
                
            }
        }
        
    });

    function stampo() {
        colori2 = colori;
        console.log(colori2);
    }
</script>

<head>
    <style>
        div{color:white}
        body {
            background-color: black;
        }
        /*----  Main Style  ----*/
        #cards_landscape_wrap-2 {
            text-align: center;
            background: rgb(51, 52, 51);
            -webkit-border-radius: 20px;
            -moz-border-radius: 20px;
            border-radius: 20px;
            padding-bottom: 3%;
        }

        h1 {
            padding-top: 2%;
            color: white;
            padding-bottom:1%;
        }
        p {
            color: white;
        }
        .immagine {
            width: 90%;
        }
        .table {
            background-color: white;
            width: 80%;
            margin: 0 auto;
            margin-top:4%;
            -webkit-border-radius: 15px;
        }
        button {
            background-color: #008cba;
        } /* Blue */
        label {
            color: white;
            float: left;
        }
        select {
            float: left;
        }
        .column {
            padding-top: 2%;
            float: left;
            width: 50%;
            padding-left: 2%;
            /* Should be removed. Only for demonstration */
        }

        /* Clear floats after the columns */
        .row:after {
            content: "";
            display: table;
            clear: both;
        }
        .dot {
            height: 25px;
            width: 25px;
            background-color: #bbb;
            border-radius: 50%;
            display: inline-block;
        }
        button {
            margin-right: 1%;
        }
        .avanti{
            float:right;
            margin-right:8%;
            margin-top: 30%;
            color:white;
            border:none
        }
        img{
            width:50%;
            height:40%;
            margin:0 auto
        }
    </style>
</head>

<div id="cards_landscape_wrap-2">
    <h1>Auto finale</h1>
    <img  src={srcFinale} alt="" />
    
    <!-- <br>
    {RiepilogoMarca}
    <br>
    {RiepilogoModello}
    <br>
    {RiepilogoMotorizzazione}
    <br>
    {RiepilogoAllestimento}
    <br>
    {RiepilogoColore} -->

    <table class="table table-borderless">
        <thead>
          <tr>
            <th scope="col">Marca</th>
            <th scope="col">Modello</th>
            <th scope="col">Motorizzazione</th>

            <th scope="col">Allestimento</th>
            <th scope="col">Colore</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            
            <td>{RiepilogoMarca}</td>
            <td>{RiepilogoModello}</td>
            <td>{RiepilogoMotorizzazione}</td>
            <td>{RiepilogoAllestimento}</td>
            <td>{RiepilogoColore}</td>
          </tr>
        </tbody>
      </table>
</div>
