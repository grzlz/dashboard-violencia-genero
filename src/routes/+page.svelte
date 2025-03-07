<script>
    import { onMount } from 'svelte';

    let texts = [
        "Violación simple: Cuando alguien obliga a otra persona (con o sin violencia) a tener una relación sexual con penetración, sin su consentimiento.",
        "Abuso sexual: Cuando alguien sin consentimiento y con contacto físico directo toca partes íntimas (senos, glúteos, genitales) de la víctima o la obliga a tocarlas.",
        "Feminicidio: Es el asesinato de una mujer por razones de género."
    ];

    let currentText = "";
    let textIndex = 0;
    let charIndex = 0;
    let isDeleting = false;
    let speed = 10; // velocidad base

    // Función para controlar el efecto de escritura y borrado
    function typeEffect() {
        const fullText = texts[textIndex];
        
        if (isDeleting) {
            currentText = fullText.substring(0, charIndex--);
            speed = 10; // más rápido al borrar
        } else {
            currentText = fullText.substring(0, charIndex++);
            speed = 25; // más lento al escribir
        }

        if (!isDeleting && charIndex === fullText.length + 1) {
            isDeleting = true;
            speed = 2000; // Pausa antes de borrar
        } else if (isDeleting && charIndex === 0) {
            isDeleting = false;
            textIndex = (textIndex + 1) % texts.length; // cambia al siguiente texto
        }

        setTimeout(typeEffect, speed);
    }

    // Al montar el componente, inicia el efecto
    onMount(() => {
        typeEffect();
    });

</script>

<style>
    .carousel {
        font-size: 1.2rem;
        font-family: 'Arial', sans-serif;
        white-space: nowrap;
        overflow: hidden;
        border-right: 2px solid #666;
        padding-right: 5px;
        animation: blink-caret 0.75s step-end infinite;
    }

    @keyframes blink-caret {
        from, to { border-color: transparent }
        50% { border-color: #666; }
    }
</style>

<div class="carousel">{currentText}</div>
