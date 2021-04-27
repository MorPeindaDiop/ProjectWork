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
    let colorSelected;
    let srcSelected = "";
    let RiepilogoModello;
    let RiepilogoMarca;
    let RiepilogoColore;
    let RiepilogoMotorizzazione;
    let RiepilogoAllestimento;
    let idColore

    onMount(async () => {
        let response = await Api.get("/colore/findAll");
        let modelli = await Api.get("/modelli/findAll");
        let marche = await Api.get("/marche/findAll");
        let motorizzazioni = await Api.get("/motorizzazioni/findAll");
        let allestimenti = await Api.get("/allestimento/findAll");

        for (let modello of modelli.result) {
            if (modello.modello == arrayUrl[3]) {
                idModello = modello.id_Modello;
            }
        }
        for (let colore of response.result) {
            if (colore.id_Modello == idModello) {
                colori.push(colore);
                idColore = colore.id_Colore;
                if (srcSelected == "") {
                    srcSelected = colore.src;
                    colorSelected = colore.descrizione;
                    
                }

                stampo();
            }
        }

        for (let motorizzazione of motorizzazioni.result) {
            if (motorizzazione.id_Motorizzazione == arrayUrl[4]) {
                RiepilogoMotorizzazione = motorizzazione.id_Motorizzazione;
            }
        }

        for (let allestimento of allestimenti.result) {
            if (allestimento.descrizione == arrayUrl[5]) {
                RiepilogoAllestimento = allestimento.id_Allestimento;
            }
        }

        for (let marca of marche.result) {
            if (marca.marca == arrayUrl[2]) {
                RiepilogoMarca = marca.id_Marca;
            }
        }
    });    


    function create(){
        let configuration={
            id_Allestimento : RiepilogoAllestimento,
            id_Colore:idColore,
            id_Marca:RiepilogoMarca,
            id_Modello:idModello,
            id_Motorizzazione:RiepilogoMotorizzazione,
            id_Utente:sessionStorage.getItem("user")
        }
        Api.post("configurazione/create",configuration)
    }

    function stampo() {
        colori2 = colori;
        console.log(colori2);
    }
</script>

<head>
    <style>
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

        h2 {
            padding-top: 2%;
            color: white;
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
        }
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
        .avanti {
            float: right;
            margin-right: 8%;
            margin-top: 30%;
            color: white;
            border: none;
        }
    </style>
</head>

<div id="cards_landscape_wrap-2">
    <h2>Scegli il colore dell'auto</h2>

    <div class="row">
        <div class="column">
            <img class="immagine" src={srcSelected} alt="" />
        </div>
        <div class="column">
            <!-- svelte-ignore a11y-label-has-associated-control -->
            <label>Colore: {colorSelected}</label>

            <br />
            <br />
            {#each colori2 as colore2}
                <button
                    on:click={() => (
                        (srcSelected = colore2.src),
                        (colorSelected = colore2.descrizione)
                    )}
                    style="background:{colore2.colore};border-radius:50%;width:60px;height:60px; float:left;text-decoration: none;border: none;outline:0"/>
                    {/each}
            <a href="{idUrl}/{colorSelected}" use:link
                ><button class="avanti" on:click="{create}">SALVA</button></a>
        </div>
    </div>
</div>
