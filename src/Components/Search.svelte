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

<main class="min-h-screen p-20 bg-[#1c1c1c] text-white flex flex-col items-center justify-start gap-8" id="formulario">

    <div class="w-full max-w-xl p-6 rounded-xl shadow-lg bg-[#3a2f2f]">
        <h1 class="lobster-font text-3xl font-bold text-center mb-6">Search Any Lyric</h1>

        <div class="space-y-4">
            <input
                class="poiret-font w-full p-2 bg-[#f5f5dc] border border-gray-600 rounded text-[#2b2b2b] placeholder-[#2b2b2b]"
                bind:value={artista}
                placeholder="Artist Name"
            />
            <input
                class="poiret-font w-full p-2 bg-[#f5f5dc] border border-gray-600 rounded text-[#2b2b2b] placeholder-[#2b2b2b]"
                bind:value={cancion}
                placeholder="Song Name"
            />
            <button
                class="lobster-font w-full bg-[#deb887] hover:bg-[#cfa36a] text-white font-semibold py-2 px-4 rounded"
                on:click={buscarLetra}
            >
                Search Lyric
            </button>
        </div>
    </div>

    {#if letra}
    <div class="flex justify-between gap-10">
        {#if mostrarPortada}
        <div class="flex flex-col justify-center bg-[#3a2f2f] p-6 rounded-xl border border-[#3a2f2f] text-white shadow-lg w-100 h-90">
            <Album {artista} {cancion} />
            <h1 class="text-2xl font-bold mt-4">{artista}</h1>
            <p class="text-lg">{cancion}</p>
        </div>
            
        {/if}
            <div class="w-full max-w-xl whitespace-pre-wrap bg-[#3a2f2f] p-6 rounded-xl border border-[#3a2f2f] text-white shadow-lg">
                {letra}
            </div>
    </div>

    {:else if error}
        <p class="text-red-400 font-medium">{error}</p>
    {/if}
</main>
