<template>
    <div class="not-found">
      <h1>404 - Página no encontrada</h1>
      <p>Lo sentimos, la página que buscas no existe.</p>
      <router-link to="/" class="home-link">Volver a la página principal</router-link>
    </div>
  </template>

  <script>
  export default {
    name: 'NotFoundView'
  };
  </script>

  <style scoped>
  .not-found {
    text-align: center;
    margin-top: 50px;
    font-family: Arial, sans-serif;
    color: #333;
  }

  .home-link {
    color: #2980b9;
    text-decoration: none;
  }

  .home-link:hover {
    text-decoration: underline;
  }
</style>