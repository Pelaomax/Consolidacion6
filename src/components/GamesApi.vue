<template>
    <div>
      <h1>Games Opinion</h1>
      <div class="games-api" v-if="games.length > 0" >
        <!-- Mostrar la lista de juegos obtenidos -->
        <div v-for="game in games" :key="game.id" class="game-card">
          <h2>{{ game.name }}</h2>
          <img :src="game.background_image" alt="Imagen del juego" class="game-image">
          <p>Rating: {{ game.rating }}</p>
          <hr>
          <p>Lanzamiento: {{game.released}}</p>
          <hr>
          <router-link :to="`/opinion/${game.name}/${encodeURIComponent(game.background_image)}`">
            <button>Opinar</button>
          </router-link>
        </div>
      </div>
      <div v-else>
        <!-- Mostrar un mensaje si no hay juegos cargados -->
        <p>Cargando juegos...</p>
      </div>
    </div>
</template>

<script>
  // Tu API key obtenida de rawg.io
  const apiKey = '5397cb3f472b462d9e59434349a1e8d2';

  // La URL base de la API
  const baseUrl = 'https://api.rawg.io/api';

  export default {
    name: 'gamesApi-comp',
    data() {
      return {
        games: [], // Array para almacenar los juegos obtenidos
      };
    },
    methods: {
      async fetchGames() {
        try {
          // Realiza una solicitud a la API para obtener una lista de juegos populares
          const response = await fetch(`${baseUrl}/games?key=${apiKey}`);

          // Verifica si la respuesta es exitosa
          if (!response.ok) {
            throw new Error('Error al obtener los datos');
          }

          // Convierte la respuesta a JSON
          const datos = await response.json();


          // Almacena los juegos en la variable de datos 'games'
          this.games = datos.results;
          console.log(this.games)
        } catch (error) {
          console.error('Error:', error);
        }
      }
    },
    mounted() {
      // Llama a la función fetchGames cuando el componente se monte
      this.fetchGames();
    }
  };
</script>

<style scoped>

  .games-api {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 16px;
    justify-items: center;
    padding: 16px;
  }

  /* Estilos básicos para los juegos */
  .game-card {
    border: 1px solid #ccc;
    padding: 16px;
    margin: 8px;
    border-radius: 8px;
    text-align: center;
  }

  .game-image {
    width: 100%;
    max-width: 300px;
    height: auto;
    margin: 16px 0;
  }
</style>