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
                <th scope="row">{{ libro.id }}</th>
                <td>{{ libro.titulo }}</td>
                <td>{{ libro.autor }}</td>
                <td>{{ libro.ISBN }}</td>
                <td>{{ libro.genero }}</td>
                <td>{{ libro.precio }}</td>
                <td>{{ libro.disponibilidad }}</td>
                <div>
                    <button @click="eliminarLibro(libro.id,libro.titulo)">
                        Eliminar
                    </button>
                </div>
            </tr>
        </tbody>
    </table>
</main>

</template>

<style scoped>
</style>