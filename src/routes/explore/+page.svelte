<script>
    import { onMount } from "svelte";

    let gifUrl = "";

    onMount(() => {
        // GIF de "Work in Progress"
        gifUrl = "https://media1.giphy.com/media/v1.Y2lkPTc5MGI3NjExMmFlMDltMTFwYzhuazdyc3FnN3QzNTI4czU0dTN3ZHE1N2h1aHphayZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/3bBFnbf2Z9lxNDkU8G/giphy.gif";
    });
</script>

<!-- HEADER CONSISTENTE CON LA PÁGINA PRINCIPAL -->
<div class="w-100 text-center py-3 text-white" style="background-color: #5a189a;">
    <h1 class="h4 fw-bold m-0">Explora los datos</h1>
</div>

<!-- CONTENIDO CON EL MISMO ESTILO QUE LA PÁGINA PRINCIPAL -->
<div class="container-fluid d-flex flex-column bg-light min-vh-100 justify-content-center align-items-center">
    <h2 class="text-dark">🚧 Work in Progress 🚧</h2>
    <p class="text-muted">Estamos trabajando en esta sección. ¡Vuelve pronto!</p>
    <img src={gifUrl} alt="Work in Progress" class="gif" />
</div>

<footer class="mt-auto text-center py-3 w-100 text-muted">
    <small>Hecho con respeto por <a href="https://www.icarus.mx" target="_blank" class="text-decoration-none text-dark fw-bold">icarus.mx</a></small>
</footer>

<style>
    .gif {
        max-width: 80%;
        height: auto;
        margin-top: 20px;
        border-radius: 10px;
    }
</style>
