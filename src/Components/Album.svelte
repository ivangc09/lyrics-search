<script>
    export let artista;
    export let cancion;

    import { onMount } from 'svelte';

    let portada = '';
    let cargando = false;

    const API_KEY = '26a9f0f85d983208cd2ed1287cd0b29b'; // <-- pon aquí tu clave

    onMount(() => {
        if (artista && cancion) {
        buscarPortada();
    }
    });

    async function buscarPortada() {
        portada = '';
        cargando = true;

        try {
            const url = `https://ws.audioscrobbler.com/2.0/?method=track.getInfo&api_key=${API_KEY}&artist=${encodeURIComponent(artista)}&track=${encodeURIComponent(cancion)}&format=json`;

            const res = await fetch(url);
            const data = await res.json();
            

            if (data.track?.album?.image?.length) {
                const imagenObj = data.track.album.image.find(img => img.size === 'extralarge') || data.track.album.image[0];
                portada = imagenObj['#text'];
            } else {
                portada = '';
            }
        } catch (e) {
            console.error('Error buscando en Last.fm', e);
        } finally {
            cargando = false;
        }
    }
</script>

{#if cargando}
    <p class="text-white">Buscando portada...</p>
{:else if portada}
    <img src={portada} alt="Portada del álbum" class="rounded-xl shadow w-94" />
{:else}
    <p class="text-red-400">Portada no encontrada</p>
{/if}
