<script>
    let imagen = '/guitarras.jpg';

    function irAlFormulario(){
        const target = document.getElementById('formulario');
        target.scrollIntoView({ behavior: 'smooth' });
    }
</script>

<div
    class="relative w-full h-[35rem] rounded-xl overflow-hidden shadow-lg bg-black"
    style="background-image: url({imagen}); background-size: cover; background-position: center;"
>
    <div class="absolute inset-0 bg-black/50 flex flex-col items-start justify-center gap-4 px-6">
        <h2 class="text-white text-[4rem] font-bold"> Find lyrics for <br /> your favorite songs </h2>
        <button on:click={irAlFormulario} class="bg-blue-600 hover:bg-blue-700 text-white px-4 py-2 rounded">Get Started</button>
    </div>
</div>