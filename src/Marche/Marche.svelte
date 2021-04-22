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
            box-shadow: 0px 2px 15px rgba(0, 0, 0, 0.5);
            border-radius: 5px;
        }
        #cards_landscape_wrap-2 .card-flyer .image-box img {
            -webkit-transition: all 0.9s ease;
            -moz-transition: all 0.9s ease;
            -o-transition: all 0.9s ease;
            -ms-transition: all 0.9s ease;
            width: 100%;
            height: 180px;
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

        h2{
            padding-top:2%;
            color:white;
        }
    </style>
</head>

<script>
    import {link} from 'svelte-spa-router';
    import { location } from 'svelte-spa-router'
    import { onMount } from 'svelte';
    export const idUrl = $location
    console.log(idUrl)
    import Api from '../Api.js';
    let marche = [];
    onMount(async () => {

const response = await Api.get('/marche/findAll')
marche=response.result
    console.log(response.result);

});
  </script>

<!-- Topic Cards -->
<div id="cards_landscape_wrap-2">
    <h2>Scelgli la marca dell'auto da configurare</h2>
    <div class="container">
        <div class="row">
            {#each marche as marca}
            <div class="col-xs-12 col-sm-6 col-md-3 col-lg-3">
                <a href="/marche/{marca.marca}" use:link>
                    <div class="card-flyer">
                        <div class="text-box">
                            <div class="image-box">
                                <img
                                    src="{marca.src}"
                                    alt=""
                                />
                            </div>
                            <div class="text-container">
                                <h6>{marca.marca}</h6>
                            </div>
                        </div>
                    </div>
                </a>
            </div>
            {/each}
            

            <!-- <div class="col-xs-12 col-sm-6 col-md-3 col-lg-3">
                <a href="#/marche/modelliBmw">
                    <div class="card-flyer">
                        <div class="text-box">
                            <div class="image-box">
                                <img
                                src="/Image/bmw.svg"
                                    alt=""
                                />
                            </div>
                            <div class="text-container">
                                <h6>Bmw</h6>
                            </div>
                        </div>
                    </div>
                </a>
            </div>
            <div class="col-xs-12 col-sm-6 col-md-3 col-lg-3">
                <a href="#/marche/modelliFord">
                    <div class="card-flyer">
                        <div class="text-box">
                            <div class="image-box">
                                <img
                                src="/Image/ford.svg"
                                    alt=""
                                />
                            </div>

                            <div class="text-container">
                                <h6>Ford</h6>
                            </div>
                        </div>
                    </div>
                </a>
            </div>
            <div class="col-xs-12 col-sm-6 col-md-3 col-lg-3">
                <a href="#/marche/modelliMercedes">
                    <div class="card-flyer">
                        <div class="text-box">
                            <div class="image-box">
                                <img
                                src="/Image/mercedes-benz.svg"
                                    alt=""
                                />
                            </div>
                            <div class="text-container">
                                <h6>Mercedes Benz</h6>
                            </div>
                        </div>
                    </div>
                </a>
            </div>
            <div class="col-xs-12 col-sm-6 col-md-3 col-lg-3">
                <a href="#/marche/modelliOpel">
                    <div class="card-flyer">
                        <div class="text-box">
                            <div class="image-box">
                                <img
                                src="/Image/opel.svg"
                                    alt=""
                                />
                            </div>
                            <div class="text-container">
                                <h6>Opel</h6>
                            </div>
                        </div>
                    </div>
                </a>
            </div>
            <div class="col-xs-12 col-sm-6 col-md-3 col-lg-3">
                <a href="#/marche/modelliPeugeot">
                    <div class="card-flyer">
                        <div class="text-box">
                            <div class="image-box">
                                <img
                                src="/Image/Peugeot.svg"
                                    alt=""
                                />
                            </div>
                            <div class="text-container">
                                <h6>Peugeot</h6>
                            </div>
                        </div>
                    </div>
                </a>
            </div>
            <div class="col-xs-12 col-sm-6 col-md-3 col-lg-3">
                <a href="#/marche/modelliRenault">
                    <div class="card-flyer">
                        <div class="text-box">
                            <div class="image-box">
                                <img
                                 src="/Image/renault.svg"
                                    alt=""
                                />
                            </div>
                            <div class="text-container">
                                <h6>Renault</h6>
                            </div>
                        </div>
                    </div>
                </a>
            </div>
            <div class="col-xs-12 col-sm-6 col-md-3 col-lg-3">
                <a href="#/marche/modelliVolkswagen">
                    <div class="card-flyer">
                        <div class="text-box">
                            <div class="image-box">
                                <img
                                src="/Image/volkswagen.svg"
                                    alt=""
                                />
                            </div>
                            <div class="text-container">
                                <h6>Volkswagen</h6>
                            </div>
                        </div>
                    </div>
                </a>
            </div> -->
        </div>
    </div>
</div>
