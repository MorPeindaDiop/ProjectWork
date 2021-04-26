<script>
    import { link } from "svelte-spa-router";
    import { location } from "svelte-spa-router";
    import { onMount } from "svelte";
    import Api from "../Api.js";
    export const idUrl = $location;
    let arrayUrl = idUrl.split("/");
    let modelli = [];
    let modelli2 = [];
    let idMarca;

    onMount(async () => {
        const response = await Api.get("/modelli/findAll");
        let marche = await Api.get("/marche/findAll");

        for (let marca of marche.result) {
            if (marca.marca == arrayUrl[arrayUrl.length - 1]) {
                idMarca = marca.id_Marca;
            }
        }
        for (let modello of response.result) {
            if (modello.id_Marca == idMarca) {
                modelli.push(modello);
                stampo();
            }
        }
    });
    function stampo() {
        modelli2 = modelli;
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
        }
        #cards_landscape_wrap-2 .card-flyer .image-box {
            background: #ffffff;
            overflow: hidden;
            box-shadow: 0px 2px 30px rgba(0, 0, 0, 0.5);
            border-radius: 5px;
        }
        #cards_landscape_wrap-2 .card-flyer .image-box img {
            -webkit-transition: all 0.9s ease;
            -moz-transition: all 0.9s ease;
            -o-transition: all 0.9s ease;
            -ms-transition: all 0.9s ease;
            width: 100%;
            height: 200px;
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
            padding: 30px 18px;
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
{#await onMount}
    <p>waiting for the promise to resolve...</p>
{:then stampo}
    <div id="cards_landscape_wrap-2">
        <h2>Scelgli la marca dell'auto da configurare</h2>
        <div class="container">
            <div class="row">
                {#each modelli2 as modello}
                    <div class="col-xs-12 col-sm-6 col-md-3 col-lg-3">
                        <a href="{idUrl}/{modello.modello}" use:link>
                            <div class="card-flyer">
                                <div class="text-box">
                                    <div class="image-box">
                                        <img src={modello.src} alt="" />
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
{/await}
