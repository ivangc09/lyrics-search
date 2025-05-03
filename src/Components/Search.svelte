<script>
    import Album from "./Album.svelte";

    let artista = '';
    let cancion = '';
    let letra = '';
    let error = '';
    let mostrarPortada = false;

    async function buscarLetra() {
        error = '';
        letra = '';
        mostrarPortada = false;

        try {
            const res = await fetch(`https://api.lyrics.ovh/v1/${artista}/${cancion}`);
            const data = await res.json();
            if (data.lyrics) {
                letra = data.lyrics;
                mostrarPortada = true;
            } else {
                error = 'Lyric not found';
            }
        } catch (e) {
            error = 'Error fetching the lyric';
        }
    }
</script>

<main class="min-h-screen p-20 bg-gray-900 text-white flex flex-col items-center justify-start gap-8" id="formulario">

    <div class="w-full max-w-xl p-6 rounded-xl shadow-lg bg-gray-800">
        <h1 class="text-3xl font-bold text-center mb-6">Search Any Lyric</h1>

        <div class="space-y-4">
            <input
                class="w-full p-2 bg-gray-700 border border-gray-600 rounded text-white placeholder-gray-400"
                bind:value={artista}
                placeholder="Artist Name"
            />
            <input
                class="w-full p-2 bg-gray-700 border border-gray-600 rounded text-white placeholder-gray-400"
                bind:value={cancion}
                placeholder="Song Name"
            />
            <button
                class="w-full bg-blue-600 hover:bg-blue-700 text-white font-semibold py-2 px-4 rounded"
                on:click={buscarLetra}
            >
                Search Lyric
            </button>
        </div>
    </div>

    {#if letra}
    <div class="flex justify-between gap-10">
        {#if mostrarPortada}
        <div class="flex flex-col justify-center bg-gray-700 p-6 rounded-xl border border-gray-600 text-white shadow-lg w-100 h-90">
            <Album {artista} {cancion} />
            <h1 class="text-2xl font-bold mt-4">{artista}</h1>
            <p class="text-lg">{cancion}</p>
        </div>
            
        {/if}
            <div class="w-full max-w-xl whitespace-pre-wrap bg-gray-700 p-6 rounded-xl border border-gray-600 text-white shadow-lg">
                {letra}
            </div>
    </div>

    {:else if error}
        <p class="text-red-400 font-medium">{error}</p>
    {/if}
</main>
