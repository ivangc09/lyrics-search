<script>
    import Header from "../../Components/Header.svelte";
</script>

<main class="bg-[#1c1c1c] min-h-screen">
    <Header />

    <div class="flex justify-around items-center p-6 gap-4">
        <div>
            <img src="musical.webp" alt="Musical Note" class="object-cover rounded-lg shadow-lg" />
        </div>
        <div class="text-white p-4">
            <h1 class="lobster-font text-2xl font-bold text-center mt-4">About Us</h1>
            <p class="poiret-font text-left mt-2">Welcome to LyricSound, your go-to platform for discovering and sharing music lyrics!</p>
            <p class="poiret-font text-left mt-2">Our mission is to provide a comprehensive database of song lyrics, making it easy for music lovers to find the words to their favorite songs.</p>
            <p class="poiret-font text-left mt-2">Whether you're looking for the latest hits or classic tunes, we've got you covered. Join us on this musical journey!</p>
        </div>
    </div>
</main>