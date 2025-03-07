<script>
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
        // Aquí puedes hacer un scroll automático o link a otra sección.
    }
</script>

<div class="container-fluid vh-100 d-flex flex-column justify-content-center bg-light">
    <!-- Barra superior -->
    <div class="row w-100 text-center py-3 bg-primary text-white">
        <h1 class="h4 fw-bold m-0">Violencia de género en Quintana Roo</h1>
    </div>

    <!-- Contenido principal -->
    <div class="d-flex flex-column justify-content-center align-items-start flex-grow-1 ps-4">
        <!-- Carrusel de texto -->
        <div class="p-4 bg-white border-start border-4 border-primary shadow-sm mb-4 text-start" style="max-width: 90%;">
            <p class="lead mb-0">{currentText}</p>
        </div>

        <!-- Botón centrado -->
        <div class="d-flex justify-content-center w-100 mt-3">
            <button class="btn btn-pink fw-bold text-center" on:click={handleExploreClick}>
                Explora los datos
            </button>
        </div>
    </div>
</div>

<style>
    :global(.btn-pink) {
        background-color: #d6336c;
        color: white;
        border: none;
    }

    :global(.btn-pink:hover) {
        background-color: #b02658;
    }

    :global(.border-primary) {
        border-color: #7b2cbf !important;
    }

    :global(.bg-primary) {
        background-color: #7b2cbf !important;
    }
</style>
