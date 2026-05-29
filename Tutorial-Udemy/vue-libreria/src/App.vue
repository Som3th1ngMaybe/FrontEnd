<script setup>
import { RouterLink, RouterView } from 'vue-router'

</script>

<template>
  <header>

    <div class="wrapper">
      <HelloWorld msg="You did it!" />

      <nav class="navbar">
        <RouterLink class="link--navbar" to="/">Libros</RouterLink>
        <RouterLink class="link--navbar" to="/NuevoLibro">Nuevo Libro</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
</template>

<style scoped>

.navbar{
  background-color: rgba(0,0 , 0, 0.1);
  margin: 10px auto;
  width: 300px;
  display: flex;
  justify-content: space-around;
  border-radius: 5px;


}

.link--navbar{
  text-decoration: none;
  padding: 10px;
  font-weight: 700;
  font-size: 1.3rem;
  color: #851515;
  transition: color 0.3s ease-in-out;
}

.link--navbar:hover{
  color:#158585
}

</style>