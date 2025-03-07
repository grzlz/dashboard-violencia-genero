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
    let speed = 50; // velocidad base

    function typeEffect() {
        const fullText = texts[textIndex];

        if (isDeleting) {
            currentText = fullText.substring(0, charIndex--);
            speed = 10; // borrar más rápido
        } else {
            currentText = fullText.substring(0, charIndex++);
            speed = 20; // escribir un poco más lento
        }

        if (!isDeleting && charIndex === fullText.length + 1) {
            isDeleting = true;
            speed = 2000; // pausa larga antes de borrar
        } else if (isDeleting && charIndex === 0) {
            isDeleting = false;
            textIndex = (textIndex + 1) % texts.length;
        }

        setTimeout(typeEffect, speed);
    }

    onMount(() => {
        typeEffect();
    });
</script>

<style>
    .carousel {
        font-size: 1.1rem;
        font-family: 'Arial', sans-serif;
        white-space: normal; /* Permitir salto de línea */
        overflow: hidden;
        max-width: 100%; /* Responsivo al contenedor */
        line-height: 1.5; /* Mejor legibilidad */
        padding: 10px;
        box-sizing: border-box;
        border-left: 4px solid #666; /* Puedes usarlo como estilo visual */
    }

    /* Estilo responsivo extra (opcional) */
    @media (max-width: 768px) {
        .carousel {
            font-size: 1rem;
            padding: 8px;
        }
    }
</style>

<div class="carousel">{currentText}</div>
