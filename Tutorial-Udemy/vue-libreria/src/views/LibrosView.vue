<script>
import axios from 'axios';
import {ref, onMounted} from 'vue';
export default {
    setup() {

        const libros = ref([]);
        const listarLibros = async () => {
            try {
                const response = await axios.get('http://localhost:3000/libros');
                libros.value = response.data;
                console.log("Libros obtenidos desde el endpoint", libros.value);
            } catch (error) {
                console.log("Error al leer los libros desde el endpoint",error);
            }
        };

        const eliminarLibro = async (id,titulo) => {
            const confirmDelete = window.confirm(`¿Estás seguro de que deseas eliminar el libro "${titulo}"?`);
            if (confirmDelete) {
                try {
                    await axios.delete(`http://localhost:3000/libros/${id}`);
                    listarLibros(); // Refrescar la lista de libros
                } catch (error) {
                    console.log("Error al eliminar el libro", error);
                }
            }
        };

        onMounted(() => {
            listarLibros();
        });

        return {
            libros,
            listarLibros,
            eliminarLibro
        }
    }
};
</script>http://localhost:3000/libros

<template>
<main>
    <table class="table table-striped">
        <thead>
            <tr>
                <th scope="col">Id</th>
                <th scope="col">Titulo</th>
                <th scope="col">Autor</th>
                <th scope="col">ISBN</th>
                <th scope="col">Genero</th>
                <th scope="col">Precio</th>
                <th scope="col">Disponibilidad</th>
                <th scope="col">Acciones</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="libro in libros" :key="libro.id">
                <th class="alinear" scope="row">{{ libro.id }}</th>
                <td>{{ libro.titulo }}</td>
                <td>{{ libro.autor }}</td>
                <td>{{ libro.ISBN }}</td>
                <td>{{ libro.genero }}</td>
                <td class="alinear">{{ libro.precio }}</td>
                <td >{{ libro.disponibilidad }}</td>
                <div class="botones">
                    <button class="btn eliminar " @click="eliminarLibro(libro.id,libro.titulo)">
                        Eliminar
                    </button>
                    <RouterLink class="btn editar" :to="{path:'/EditarLibro/'+libro.id}">Editar</RouterLink>
                </div>
            </tr>
        </tbody>
    </table>
</main>
</template>

<style scoped>

table{
    width: 90%;
    border-collapse: collapse;
    margin: 10px auto;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.2);
}

td, th{
    border: 1px solid #000;
    padding: 10px;

}

th {
    background-color: #dddada;
}

.alinear{
    text-align: center;
}

.botones{
    display: flex;
    justify-content: space-around;
    border: solid 1 px #000;
}

.btn{
    background-color: transparent;
    border: none;
    padding: 10px 15 px;
    text-decoration: none;
    font-family: "UnifrakturMaguntia", cursive;
    color: #000;
    font-size: 1rem;
    border-radius: 5px;
    cursor: pointer;
    margin: 5px;
}

.editar{
    background-color: orange;
    color: #fff;
    transition: background-color 0.3s ease-in-out;
}

.eliminar{
    background-color: red;
    color: #fff;
    transition: background-color 0.3s ease-in-out;
}

.eliminar:hover{
    background-color: crimson;
}
.editar:hover{
    background-color: darkgoldenrod;
}

</style>