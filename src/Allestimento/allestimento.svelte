<script>
    import { link } from "svelte-spa-router";
    import { location } from "svelte-spa-router";
    import { onMount } from "svelte";
    import Api from "../Api.js";
    export let idUrl = $location;
    idUrl = idUrl.replace(/%20/g, " ");
    console.log(idUrl);
    let arrayUrl = idUrl.split("/");
    console.log(arrayUrl);
    let allestimenti = [];
    let allestimenti2 = [];
    let idModello;
    let modelloProva;

    onMount(async () => {
        let response = await Api.get("/allestimento/findAll");
        let modelli = await Api.get("/modelli/findAll");
        console.log(response.result);

        for (let modello of modelli.result) {
            if (modello.modello == arrayUrl[3]) {
                idModello = modello.id_Modello;
                modelloProva = modello;
            }
        }
        for (let allestimento of response.result) {
            if (allestimento.id_Modello == idModello) {
                allestimenti.push(allestimento);
                stampo();
            }
        }
    });
    function stampo() {
        allestimenti2 = allestimenti;
        console.log(allestimenti2);
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
            padding-top: 2%;
            padding-bottom: 2%;
            width: 40%;
            height: 40%;
        }
        .table {
            background-color: white;
            width: 40%;
            margin: 0 auto;
            -webkit-border-radius: 15px;
        }
        .table th {
            border-top: 0px !important;
        }
        button {
            background-color: #008cba;
            color: white;
        }
        p {
            color: white;
        }
    </style>
</head>

<div id="cards_landscape_wrap-2">
    {#if modelloProva != undefined}
        <img class="immagine" src={modelloProva.src} alt="" />
        <table class="table table-hover">
            <thead>
                <tr>
                    <th scope="col">Allestimento</th>
                </tr>
            </thead>
            <tbody>
                {#each allestimenti2 as allestimenti}
                    <tr>
                        <td>{allestimenti.descrizione}</td>
                        <td>
                            <a
                                href="{idUrl}/{allestimenti.descrizione}"
                                use:link>
                                <button>SELEZIONA</button>
                            </a></td>
                    </tr>
                {/each}
            </tbody>
        </table>
    {/if}
</div>
