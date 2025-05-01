<script>
    let artista = '';
    let cancion = '';
    let letra = '';
    let error = '';

    async function buscarLetra() {
        error = '';
        letra = '';
        try {
            const res = await fetch(`https://api.lyrics.ovh/v1/${artista}/${cancion}`);
            const data = await res.json();
            if (data.lyrics) {
                letra = data.lyrics;
            } else {
                error = 'Lyric not found';
            }
        } catch (e) {
            error = 'Error fetching the lyric';
        }
    }
</script>

<main class="p-20 bg-gray-900 text-white flex items-center justify-center">
    
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

        {#if letra}
            <pre class="whitespace-pre-wrap mt-6 bg-gray-700 p-4 rounded border border-gray-600 text-white">{letra}</pre>
        {:else if error}
            <p class="mt-6 text-red-400 font-medium">{error}</p>
        {/if}
    </div>
</main>