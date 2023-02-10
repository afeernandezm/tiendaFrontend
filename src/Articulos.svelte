<script>
    import { onMount } from "svelte";
    import Buscar from "./Buscar.svelte";
    let data = [];
    let datosFiltrados = [];
    let patron = "Camisa";
    let getArticulos = async () => {
        const response = await fetch(
            "https://tiendabackend.fly.dev/api/articulos/"
        );
        data = await response.json();
    };
    onMount(getArticulos);
    $: datosFiltrados = data.filter((articulo) =>
        RegExp(patron, "i").test(articulo.nombre)
    );
</script>

<Buscar bind:busqueda={patron} />
<hr />
{#each datosFiltrados as articulo}
    {articulo.nombre} <br />

    <b>Precio: </b>
    {articulo.precio}<br /><br />
    <hr />
{/each}
