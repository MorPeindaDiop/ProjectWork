<script>
	import { link } from "svelte-spa-router";
	import Router from "svelte-spa-router";
	import Home from "./Home/Home.svelte";

	import Login from "./Login/Login.svelte";
	import About from "./About/About.svelte";
	import Marche from "./Marche/Marche.svelte";
	import Modelli from "./Modelli/modelli.svelte";
	import Motorizzazione from "./Motorizzazione/Motorizzazione.svelte";
	import Allestimento from "./Allestimento/allestimento.svelte";
	import Colore from "./colore/colore.svelte";
	import Configurazione from "./RiepilogoAuto/configurazione.svelte";
	import { wrap } from 'svelte-spa-router/wrap'
	import { location, replace } from 'svelte-spa-router'
	import { afterUpdate } from 'svelte';
	import { onMount } from 'svelte';
import Auto from "./Auto/Auto.svelte";
	let url
	url = $location



	let log = ''
	const routes = {
		'/login': wrap({
			component: Login,
			guards: [userIsLogged()],
		}),
		//"/": Home,
		'/home': wrap({
			component: Home,
			guards: [userIsNotLogged()],
            redirect: '/Home'
		}),
		"/about": About,
		"/auto": Auto,
		//"/login": Login,
		"/marche": Marche,
		"/marche/:marca": Modelli,
		"/marche/:marca/:modello": Motorizzazione,
		"/marche/:marca/:modello/:motorizzazione": Allestimento,
		"/marche/:marca/:modello/:motorizzazione/:allestimento": Colore,
		"/marche/:marca/:modello/:motorizzazione/:allestimento/:colore": Configurazione,
		
	}
	function userIsNotLogged() {
		if (sessionStorage.getItem('user') != null) {
			return true
		}
		replace('/Home')
		return false
	}
	function userIsLogged() {
		if (sessionStorage.getItem('user') == null) {
			return true
		}
		return false
	}

	function logout() {
		sessionStorage.clear()
	}

	onMount(async () => {
        
    });
	afterUpdate(() => {
		console.log('the component just updated');
		url = $location;
    	console.log(url)

		if (sessionStorage.getItem('user')!= null) {
			log = 'logout'
		} else {
			log = 'login'
		}
	});
	

	
	
</script>

<head>
	<link
		rel="stylesheet"
		href="https://maxcdn.bootstrapcdn.com/font-awesome/4.5.0/css/font-awesome.min.css"/></head>

{#if url != '/login'}
<nav class="navbar navbar-expand-md navbar-dark bg-black">
	<div
		class="navbar-collapse collapse w-100 order-1 order-md-0 dual-collapse2"
	>
		<ul class="navbar-nav mr-auto">
			<li class="nav-item active">
				<a class="nav-link" href="/home" use:link>Home</a>
			</li>
			<li class="nav-item">
				<a class="nav-link" href="/about" use:link>About</a>
			</li>
			{#if log=='logout'}
			<li class="nav-item">
				<a class="nav-link" href="/auto" use:link>Auto</a>
			</li>
			{/if}
		</ul>
	</div>
	<div class="mx-auto order-0">
		<a class="navbar-brand mx-auto" href="#">
			<img src="/Image/logo.png" alt="" width="200" height="70" />
		</a>
		<button
			class="navbar-toggler"
			type="button"
			data-toggle="collapse"
			data-target=".dual-collapse2"
		>
			<span class="navbar-toggler-icon" />
		</button>
	</div>
	<div class="navbar-collapse collapse w-100 order-3 dual-collapse2">
		<ul class="navbar-nav ml-auto">
			<li class="nav-item">
				<a class="nav-link" href="/login" use:link on:click="{logout}">{log.toUpperCase()}</a>
			</li>
		</ul>
	</div>
</nav>
<div class="col-md-12 copy" />
{/if}



<main>
	<!-- <h1>Hello {name}!</h1>
	<p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p> -->

	<Router {routes} />
</main>

{#if url != '/login'}
<footer class="mainfooter" role="contentinfo">
	<div class="footer-middle">
		<div class="container">
			<div class="row">
				<div class="col-md-3 col-sm-6">
					<!--Column1-->
					<div class="footer-pad">
						<h4>Modelli</h4>
						<ul class="list-unstyled">
							<li><a href="#">Panoramica modelli</a></li>
							<li><a href="#">Configuratore</a></li>
						</ul>
					</div>
				</div>
				<div class="col-md-3 col-sm-6">
					<!--Column1-->
					<div class="footer-pad">
						<h4>Servizi</h4>
						<ul class="list-unstyled">
							<li class="colore">
								<a href="#">Website Tutorial</a>
							</li>
							<li class="colore">
								<a href="#">Accessibility</a>
							</li>
							<li class="colore"><a href="#">Disclaimer</a></li>
							<li class="colore">
								<a href="#">Privacy Policy</a>
							</li>
							<li class="colore"><a href="#">FAQs</a></li>
							<li class="colore"><a href="#">Webmaster</a></li>
						</ul>
					</div>
				</div>
				<div class="col-md-3 col-sm-6">
					<!--Column1-->
					<div class="footer-pad">
						<h4>Contattaci</h4>
						<ul class="list-unstyled">
							<li><a href="#">Parks and Recreation</a></li>
							<li><a href="#">Public Works</a></li>
							<li><a href="#">Police Department</a></li>
							<li><a href="#">Fire</a></li>
							<li><a href="#">Mayor and City Council</a></li>
							<li>
								<a href="#" />
							</li>
						</ul>
					</div>
				</div>
				<div class="col-md-3">
					<h4>Showroom</h4>
					<ul class="social-network social-circle">
						<li>
							<a
								href="https://www.facebook.com/"
								class="icoFacebook"
								title="Facebook"><i class="fa fa-facebook" /></a>
						</li>
						<li>
							<a
								href="https://twitter.com/?lang=it"
								class="icoTwitter"
								title="Twitter"><i class="fa fa-twitter" /></a>
						</li>
						<li>
							<a
								href="https://it.linkedin.com/"
								class="icoLinkedin"
								title="Linkedin"><i class="fa fa-linkedin" /></a>
						</li>
					</ul>
				</div>
			</div>
			<div class="row">
				<div class="col-md-12 copy">
					<p class="text-center colore">
						&copy; Copyright 2021 - Diop car service. All rights
						reserved.
					</p>
				</div>
			</div>
		</div>
	</div>
</footer>
{/if}

<style>
	nav {
		font-size: 20px;
	}
	.logo {
		margin: 0 auto;
	}
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}

	/*FOOTER*/

	footer {
		background: black;

		color: white;
		margin-top: 100px;
	}

	footer a {
		color: gray;
		font-size: 14px;
		transition-duration: 0.2s;
	}

	footer a:hover {
		color: white;
		text-decoration: none;
	}

	.copy {
		font-size: 12px;
		padding: 10px;
		border-top: 1px solid gray;
	}

	.footer-middle {
		padding-top: 2em;
		color: white;
	}

	/*SOCİAL İCONS*/

	/* footer social icons */

	ul.social-network {
		list-style: none;
		display: inline;
		margin-left: 0 !important;
		padding: 0;
	}

	ul.social-network li {
		display: inline;
		margin: 0 5px;
	}

	/* footer social icons */

	.social-network a.icoFacebook:hover {
		background-color: #3b5998;
	}

	.social-network a.icoLinkedin:hover {
		background-color: #007bb7;
	}

	.social-network a.icoFacebook:hover i,
	.social-network a.icoLinkedin:hover i {
		color: #fff;
	}

	.social-network a.socialIcon:hover,
	.socialHoverClass {
		color: #44bcdd;
	}

	.social-circle li a {
		display: inline-block;
		position: relative;
		margin: 0 auto 0 auto;
		-moz-border-radius: 50%;
		-webkit-border-radius: 50%;
		border-radius: 50%;
		text-align: center;
		width: 30px;
		height: 30px;
		font-size: 15px;
	}

	.social-circle li i {
		margin: 0;
		line-height: 30px;
		text-align: center;
	}

	.social-circle li a:hover i,
	.triggeredHover {
		-moz-transform: rotate(360deg);
		-webkit-transform: rotate(360deg);
		-ms--transform: rotate(360deg);
		transform: rotate(360deg);
		-webkit-transition: all 0.2s;
		-moz-transition: all 0.2s;
		-o-transition: all 0.2s;
		-ms-transition: all 0.2s;
		transition: all 0.2s;
	}

	.social-circle i {
		color: #595959;
		-webkit-transition: all 0.8s;
		-moz-transition: all 0.8s;
		-o-transition: all 0.8s;
		-ms-transition: all 0.8s;
		transition: all 0.8s;
	}

	.social-network a {
		background-color: #f9f9f9;
	}
	.colore {
		color: gray;
	}
</style>
