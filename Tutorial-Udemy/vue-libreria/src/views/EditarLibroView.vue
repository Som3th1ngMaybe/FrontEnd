<script>
import {ref,onMounted} from "vue";
import axios from "axios";
import { useRoute, useRouter } from "vue-router";
import router from "@/router";

export default {
    setup(){
        const editarLibro = ref ({
            id:null,
            titulo:'',
            autor:'',
            ISBN:'',
            genero:'',
            precio:'',
            disponibilidad:''
        });

        const CargarLibro = async () => {
            const libroId = useRoute().params.id
            try {
                const response = await axios.get(`http://localhost:3000/libros/${libroId}`)
                editarLibro.value = response.data
                console.log(editarLibro.value)
            } catch (error) {
                console.log("Error al cargar el libro a editar",error)
            }
        }

        const ActualizarLibro = async () => {
            try {
                const response = await axios.put(`http://localhost:3000/libros/${editarLibro.value.id}`, editarLibro.value);

                setTimeout(() => {
                    alert("Libro actualizado con éxito") 
                }, 200);

                router.push('/')
                console.log('Libro creado con exito',response.data)
            } catch (error) {
                console.log("Error al actualizar el libro",error)
            }
        };

        onMounted(() => {
            CargarLibro();
        });

        return{
            editarLibro,
            ActualizarLibro,
            CargarLibro
    };
}
}

</script>

<template>
    <main>
        <form @submit.prevent="ActualizarLibro">
            <div>
                <label for="titulo">titulo</label>
                <input name ="titulo" v-model="editarLibro.titulo"  type="text" required placeholder="Titulo">
            </div>

            <div>
                <label for="autor">autor</label>
                <input name ="autor" v-model="editarLibro.autor"  type="text" required placeholder="Autor">
            </div>

            <div>
                <label for="isbn">isbn</label>
                <input name="isbn" v-model="editarLibro.ISBN"  type="text" required placeholder="ISBN">
            </div>

            <div>
                <label for="genero">genero</label>
                <input name="genero" v-model="editarLibro.genero"  type="text" required placeholder="Género">
            </div>

            <div>
                <label for="precio">precio</label>
                <input name="precio" v-model="editarLibro.precio"  type="text" required placeholder="Precio">
            </div>

            <div>
                <label for="disponibilidad">disponibilidad</label>
                <input name="disponibilidad" v-model="editarLibro.disponibilidad"  type="text" required placeholder="Disponibilidad">
            </div>
            <button type="submit">Guardar Cambios Libro</button>
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