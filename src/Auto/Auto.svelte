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
    let idConfigurazione;
    // let idModello;
    let riepilogoModello;
    let riepilogoMarca;
    let riepilogoColore;
    let riepilogoMotorizzazione;
    let riepilogoAllestimento;
    let riepilogoSrc="";
    // let srcFinale = "";

    let utente;
    let cards = [];
    let cards2 = [];

    onMount(async () => {
        let configurazioni = await Api.get("/configurazione/findAll");

        let colori = await Api.get("/colore/findAll");
        let modelli = await Api.get("/modelli/findAll");
        let marche = await Api.get("/marche/findAll");
        let motorizzazioni = await Api.get("/motorizzazioni/findAll");
        let allestimenti = await Api.get("/allestimento/findAll");
        
        console.log(configurazioni.result)
        for (let configurazione of configurazioni.result) {
           
            if(configurazione.id_Utente==sessionStorage.getItem("user")){
               
                for (let allestimento of allestimenti.result) {
                    if (allestimento.id_Allestimento ==configurazione.id_Allestimento) {
                         riepilogoAllestimento = allestimento.descrizione;
                    }
                }
                for (let colore of colori.result) {
                    if (colore.id_Colore ==configurazione.id_Colore) {
                         riepilogoColore = colore.descrizione;
                         riepilogoSrc=colore.src
                    }
                }

                for (let marca of marche.result) {
                    if (marca.id_Marca ==configurazione.id_Marca) {
                         riepilogoMarca = marca.marca;
                    }
                }

                for (let modello of modelli.result) {
                    if (modello.id_Modello ==configurazione.id_Modello) {
                         riepilogoModello = modello.modello;
                    }
                }

                for (let motorizzazione of motorizzazioni.result) {
                    if (motorizzazione.id_Motorizzazione ==configurazione.id_Motorizzazione) {
                         riepilogoMotorizzazione = motorizzazione.motore;
                    }
                }
                let riepilogo={
                    allestimento : riepilogoAllestimento,
                    colore : riepilogoColore,
                    marca : riepilogoMarca,
                    modello:riepilogoModello,
                    motorizzazione:riepilogoMotorizzazione,
                    src:riepilogoSrc
                }
                cards.push(riepilogo)
                
            }
            stampo()
        }
        console.log(cards)

        
    });

    function stampo() {
        cards2=cards
    }
</script>

<head>
    <style>
        h6{color:white}
        div {
            color: white;
        }
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
            padding-bottom: 1%;
        }
        p {
            color: white;
        }
        .immagine {
            width: 50%;
            height: 40%;
            margin: 0 auto;
        }
        .table {
            background-color: white;
            width: 80%;
            margin: 0 auto;
            margin-top: 4%;
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
        }
        #cards_landscape_wrap-2 .container {
            padding-bottom: 100px;
        }
        #cards_landscape_wrap-2 a {
            text-decoration: none;
            outline: none;
        }
        #cards_landscape_wrap-2 .card-flyer {
            border-radius: 5px;
            width:350px
        }
        #cards_landscape_wrap-2 .card-flyer .image-box {
            background: #ffffff;
            overflow: hidden;
            box-shadow: 0px 2px 15px rgba(0, 0, 0, 0.5);
            border-radius: 5px;
        }
        #cards_landscape_wrap-2 .card-flyer .image-box img {
            -webkit-transition: all 0.9s ease;
            -moz-transition: all 0.9s ease;
            -o-transition: all 0.9s ease;
            -ms-transition: all 0.9s ease;
            width: 100%;
            height: 250px;
        }
        #cards_landscape_wrap-2 .card-flyer:hover .image-box img {
            opacity: 0.7;
            -webkit-transform: scale(1.15);
            -moz-transform: scale(1.15);
            -ms-transform: scale(1.15);
            -o-transform: scale(1.15);
            transform: scale(1.15);
        }
        #cards_landscape_wrap-2 .card-flyer .text-box {
            text-align: center;
        }
        #cards_landscape_wrap-2 .card-flyer .text-box .text-container {
            padding: 10px 18px;
        }
        #cards_landscape_wrap-2 .card-flyer {
            background: #ffffff;
            margin-top: 50px;
            -webkit-transition: all 0.2s ease-in;
            -moz-transition: all 0.2s ease-in;
            -ms-transition: all 0.2s ease-in;
            -o-transition: all 0.2s ease-in;
            transition: all 0.2s ease-in;
            box-shadow: 0px 3px 4px rgba(0, 0, 0, 0.4);
        }
        #cards_landscape_wrap-2 .card-flyer:hover {
            background: #fff;
            box-shadow: 0px 15px 26px rgba(0, 0, 0, 0.5);
            -webkit-transition: all 0.2s ease-in;
            -moz-transition: all 0.2s ease-in;
            -ms-transition: all 0.2s ease-in;
            -o-transition: all 0.2s ease-in;
            transition: all 0.2s ease-in;
            margin-top: 50px;
        }
        #cards_landscape_wrap-2 .card-flyer .text-box p {
            margin-top: 10px;
            margin-bottom: 0px;
            padding-bottom: 0px;
            font-size: 14px;
            letter-spacing: 1px;
            color: #000000;
        }
        #cards_landscape_wrap-2 .card-flyer .text-box h6 {
            margin-top: 0px;
            margin-bottom: 4px;
            font-size: 18px;
            font-weight: bold;
            font-family: "Roboto Black", sans-serif;
            letter-spacing: 1px;
            color: #00acc1;
        }

        h2 {
            padding-top: 2%;
            color: white;
        }
    </style>
</head>

<div id="cards_landscape_wrap-2">
    <h1>Le tue auto configurate</h1>

    <div id="cards_landscape_wrap-2">
        <div class="container">
            
            <div class="row">
            {#if cards2.length!=0}
            {#each cards2 as card}
                <div class="col-xs-12 col-sm-6 col-md-3 col-lg-4">
                    
                        <div class="card-flyer" >
                            <div class="text-box">
                                <div class="image-box">
                                    <img src={card.src} alt="" />
                                </div>
                                <div class="text-container">
                                    <h6>{card.colore}</h6>
                                </div>
                                <div class="text-container">
                                    <h6>{card.motorizzazione}</h6>
                                </div>
                                <div class="text-container">
                                    <h6>{card.marca}</h6>
                                </div>
                                <div class="text-container">
                                    <h6>{card.modello}</h6>
                                </div>
                                <div class="text-container">
                                    <h6>{card.allestimento}</h6>
                                </div>

                            </div>
                        </div>

                </div>
                {/each}
                {/if}
        </div>
    </div>
    </div>
    
</div>
