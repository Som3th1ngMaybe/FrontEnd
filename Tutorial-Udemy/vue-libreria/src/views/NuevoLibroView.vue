<script>
import {ref} from "vue";
import axios from "axios";
export default {
    setup(){

        const nuevoLibro = ref ({
            titulo:'',
            autor:'',
            ISBN:'',
            genero:'',
            precio:'',
            disponibilidad:''
        });

        const CrearLibro = async () => {
            try {
                const response = await axios.post("http://localhost:3000/libros/",nuevoLibro.value);

                setTimeout(() => {
                    alert("Libro creado con éxito") 
                }, 200);

                nuevoLibro.value.titulo='',
                nuevoLibro.value.autor='',
                nuevoLibro.value.ISBN='',
                nuevoLibro.value.genero='',
                nuevoLibro.value.precio='',
                nuevoLibro.value.disponibilidad=''

                console.log('Libro cread con exito',response.data)
            } catch (error) {
                console.log("No se pudo crear el libro",error)
            }
        };

        return{
            nuevoLibro,
            CrearLibro
        };
    }
}

</script>

<template>
    <main>
        <form @submit.prevent="CrearLibro">
            <div>
                <label for="titulo">titulo</label>
                <input name ="titulo" v-model="nuevoLibro.titulo"  type="text" required placeholder="Titulo">
            </div>

            <div>
                <label for="autor">autor</label>
                <input name ="autor" v-model="nuevoLibro.autor"  type="text" required placeholder="Autor">
            </div>

            <div>
                <label for="isbn">isbn</label>
                <input name="isbn" v-model="nuevoLibro.ISBN"  type="text" required placeholder="ISBN">
            </div>

            <div>
                <label for="genero">genero</label>
                <input name="genero" v-model="nuevoLibro.genero"  type="text" required placeholder="Género">
            </div>

            <div>
                <label for="precio">precio</label>
                <input name="precio" v-model="nuevoLibro.precio"  type="text" required placeholder="Precio">
            </div>

            <div>
                <label for="disponibilidad">disponibilidad</label>
                <input name="disponibilidad" v-model="nuevoLibro.disponibilidad"  type="text" required placeholder="Disponibilidad">
            </div>
            <button class="btn enviar" type="submit">Crear Nuevo Libro</button>
        </form>
    </main>
</template>

<style scoped>

form{
    width: 90%;
    margin: 25px auto;
    padding: 20px;
    border: solid 1px #000;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.2);

}

label{
    font-weight: bold;
    margin-bottom: 5px;
    display: block;
    font-size: 1rem;
}

input{
    font-weight: bold;
    width: 100%;
    padding: 5px;
    border: solid 1px #000;
    margin-bottom: 15px;
    font-family: "UnifrakturMaguntia", cursive;
    font-size: 1rem;
}

input:focus{
    outline: none;
}

.btn{
    background-color: transparent;
    border: none;
    padding: 10px 15px;
    text-decoration: none;
    font-family: "UnifrakturMaguntia", cursive;
    color: #000;
    font-size: 1rem;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease-in-out;
    margin: 5px;
    width: 100px;
}

.enviar{
    background-color: greenyellow;
    color: whitesmoke;
}

.enviar:hover{
    background-color: green;
}

</style>