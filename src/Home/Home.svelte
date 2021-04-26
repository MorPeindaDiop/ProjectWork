<script>
  import { link } from "svelte-spa-router";
</script>

<head>
  <style>
    body {
      background-color: black;
    }
    .paragrafo {
      font-size: 20px;
      color: white;
      font-family: Arial, Helvetica, sans-serif;
    }
  </style>
</head>

<p class="paragrafo">Diop car service</p>
<br />
<div id="carouselExampleIndicators" class="carousel slide" data-ride="carousel">
  <ol class="carousel-indicators">
    <li
      data-target="#carouselExampleIndicators"
      data-slide-to="0"
      class="active"/>
    <li data-target="#carouselExampleIndicators" data-slide-to="1" />
    <li data-target="#carouselExampleIndicators" data-slide-to="2" />
  </ol>
  <div class="carousel-inner">
    <div class="carousel-item active">
      <img class="d-block w-100" src="/Image/peugeot1.jpg" alt="First slide" />
    </div>
    <div class="carousel-item">
      <img class="d-block w-100" src="/Image/golf8.jpg" alt="Second slide" />
    </div>
    <div class="carousel-item">
      <img class="d-block w-100" src="/Image/opel.jpeg" alt="Third slide" />
    </div>
  </div>
  <a
    class="carousel-control-prev"
    href="#carouselExampleIndicators"
    role="button"
    data-slide="prev">
    <span class="carousel-control-prev-icon" aria-hidden="true" />
    <span class="sr-only">Previous</span>
  </a>
  <a
    class="carousel-control-next"
    href="#carouselExampleIndicators"
    role="button"
    data-slide="next">
    <span class="carousel-control-next-icon" aria-hidden="true" />
    <span class="sr-only">Next</span>
  </a>
</div>
<br>
<br>
<a href="/marche" use:link>
  <button
    type="button"
    class="btn btn-primary"
    data-toggle="button"
    aria-pressed="false"
    autocomplete="off">CONFIGURA LA TUA AUTO</button></a>
