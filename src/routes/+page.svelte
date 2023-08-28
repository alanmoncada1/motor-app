<script>
// @ts-nocheck

    const unsplashUrl = "https://api.unsplash.com/photos?client_id=WFiHJQhB47SgslCVZswPk1tubzVypdmTGInc_4XkA5A";
    
    async function getImagesFrom() {
        const unsplashPromise = await fetch(unsplashUrl);
        const data = await unsplashPromise.json();
        let images = [];

        // Extract data from unsplash API    
        data.forEach(element => {
            const { id, urls } = element;
            const { raw, full, regular, small } = urls;

            images.push({id, raw, full, regular, small});
        });

        return images;
    }

    
    // function seedData() {
    //     const imageStr = "https://images.unsplash.com/photo-1438761681033-6461ffad8d80?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=2070&q=80"
    //     let images = [];

    //     for (let i = 0; i < 8; i++) {
    //         images.push({
    //             id: i,
    //             raw: imageStr,
    //             full: imageStr,
    //             regular: imageStr,
    //             small: imageStr,
    //         });
    //     }

    //     return images;
    // }
    const imagesPromise = getImagesFrom();
    debugger

</script>



<div class="image-container">
    {#await imagesPromise then images } 
        {#each images as image }
            <div class="container-element">
                <img src={image.raw} alt="">
            </div>
        {/each}
    {/await}
</div>

<style>
    .image-container {
        flex-wrap: wrap; /* Permite que los elementos se envuelvan en múltiples filas */
        justify-content: space-around; /* Da espacio alrededor de cada imagen */
        /* gap: 10px; Espacio entre las imagenes */
        max-width: 100%;
        padding: 5px; /* Espaciado alrededor del contenedor principal */
    }
    .container-element {
        margin: 8px; /* Margen alrededor de cada imagen */
        max-width: calc(40% - 100px); /* Suponiendo que deseas 4 imágenes por fila, ajusta según tus necesidades */
        position: relative; /* Esto será útil si decides agregar overlays o más contenido sobre las imágenes más tarde */
    }
    .container-element img {
        width: 100%; /* La imagen se estirará para llenar su contenedor */
        height: 250px; /* Mantiene la relación de aspecto */
        object-fit: cover; /* Asegura que la imagen cubra todo el espacio sin distorsionarse */
        border-radius: 8px; /* Bordes redondeados */
    } 

    @media (max-width: 620px) {
        .image-container {
            display: grid;
            max-width: 100%;
            padding: 5px; /* Espaciado alrededor del contenedor principal */
        }
        .container-element {
            margin: 8px; /* Margen alrededor de cada imagen */
            max-width: 100%; /* Suponiendo que deseas 4 imágenes por fila, ajusta según tus necesidades */
            position: relative; /* Esto será útil si decides agregar overlays o más contenido sobre las imágenes más tarde */
        }
    }
</style>