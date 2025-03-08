<script>
	import { goto } from '$app/navigation';
    import { onMount } from 'svelte';

    let texts = [
        "Violación simple: cuando alguien obliga a otra persona (con o sin violencia) a tener una relación sexual con penetración, sin su consentimiento.",
        "Abuso sexual: cuando alguien sin consentimiento y con contacto físico directo toca partes íntimas (senos, glúteos, genitales) de la víctima o la obliga a tocarlas.",
        "Feminicidio: es el asesinato de una mujer por razones de género. Se considera feminicidio cuando la víctima es asesinada por ser mujer y existen elementos como antecedentes de violencia, amenazas, abuso sexual, mutilaciones, o exposición pública del cuerpo."
    ];

    let currentText = "";
    let textIndex = 0;
    let charIndex = 0;
    let isDeleting = false;
    let speed = 50;

    function typeEffect() {
        const fullText = texts[textIndex];

        if (isDeleting) {
            currentText = fullText.substring(0, charIndex--);
            speed = 10;
        } else {
            currentText = fullText.substring(0, charIndex++);
            speed = 20;
        }

        if (!isDeleting && charIndex === fullText.length + 1) {
            isDeleting = true;
            speed = 2000;
        } else if (isDeleting && charIndex === 0) {
            isDeleting = false;
            textIndex = (textIndex + 1) % texts.length;
        }

        setTimeout(typeEffect, speed);
    }

    onMount(() => {
        typeEffect();
    });

    function handleExploreClick() {
        console.log('Explora los datos clickeado');
        goto('/explore');
    }
</script>



<div class="w-100 text-center py-3 text-white" style="background-color: #5a189a;">
    <h1 class="h4 fw-bold m-0">Violencia de género en Quintana Roo</h1>
</div>

<div class="container-fluid d-flex flex-column bg-light min-vh-100">
    <!-- Contenido principal -->
    <div class="d-flex flex-column align-items-start ps-4 pt-4">
        <!-- Carrusel de texto -->
        <div class="p-4 mt-3 mb-4 text-start" style="height: 360px; overflow: hidden;">
            <p class="lead mb-0">{currentText}</p>
        </div>
        

        <div class="d-flex flex-column align-items-center gap-2 w-100">
            <button class="btn btn-pink fw-bold text-center w-100" style="max-width: 300px;" on:click={handleExploreClick}>
                Explora los datos
            </button>
            <a class="btn btn-purple fw-bold text-center w-100" style="max-width: 300px;" href="https://semujeres.qroo.gob.mx/" target="_blank">
                Pide ayuda
            </a>
        </div>
    </div>
</div>

<footer class="mt-auto text-center py-3 w-100 text-muted">
    <small>Hecho con respeto por <a href="https://www.icarus.mx" target="_blank" class="text-decoration-none text-dark fw-bold">icarus.mx</a></small>
</footer>


<style>
    :global(.btn-pink) {
        background-color: #d6336c;
        color: white;
        border: none;
        padding: 12px 24px;
        font-size: 1rem;
        border-radius: 5px;
        text-transform: uppercase;
        font-weight: bold;
        transition: background-color 0.3s;
    }

    :global(.btn-pink:hover) {
        background-color: #b02658;
    }

    :global(.btn-purple) {
        background-color: #5a189a;
        color: white;
        border: none;
        padding: 12px 24px;
        font-size: 1rem;
        border-radius: 5px;
        text-transform: uppercase;
        font-weight: bold;
        transition: background-color 0.3s;
    }

    :global(.btn-purple:hover) {
        background-color: #3c096c;
    }
</style>


