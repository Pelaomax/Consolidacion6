<template>
    <div class="App">
      <h1>Opinión sobre {{ gameName }}</h1>
      <img :src="gameImg" alt="Imagen del juego" class="game-img">

      <!-- Inputs para nombre y opinión -->
      <div class="opinion-form">
        <input
          type="text"
          placeholder="Tu nombre"
          v-model="newOpinion.name"
          class="input-field"
        />
        <textarea
          placeholder="Escribe tu opinión aquí..."
          v-model="newOpinion.comment"
          class="textarea-field"
        ></textarea>
        <button @click="addOrUpdateOpinion" class="submit-btn">
          {{ editIndex !== null ? 'Actualizar Opinión' : 'Enviar Opinión' }}
        </button>
      </div>

      <!-- Listado de opiniones -->
      <div class="opinions-list">
        <h2>Opiniones</h2>
        <div
          v-for="(opinion, index) in opinions"
          :key="index"
          class="opinion-card"
        >
          <div class="opinion-header">
            <h3>{{ opinion.name }}</h3>
            <div class="opinion-actions">
              <button @click="editOpinion(index)" class="edit-btn">Editar</button>
              <button @click="deleteOpinion(index)" class="delete-btn">Eliminar</button>
            </div>
          </div>
          <p>{{ opinion.comment }}</p>
        </div>
      </div>
    </div>
  </template>

  <script>
  export default {
    name: 'OpinionView',
    data() {
      return {
        newOpinion: {
          name: '',
          comment: '',
        },
        opinions: [],
        editIndex: null // Para saber si estamos editando una opinión
      };
    },
    computed: {
      gameName() {
        return this.$route.params.gameName;
      },
      gameImg() {
        return decodeURIComponent(this.$route.params.gameImg);
      }
    },
    methods: {
      addOrUpdateOpinion() {
        if (this.newOpinion.name.trim() === '' || this.newOpinion.comment.trim() === '') {
          alert('Por favor, completa ambos campos antes de enviar.');
          return;
        }

        if (this.editIndex !== null) {
          // Actualiza la opinión existente
          this.opinions[this.editIndex] = { ...this.newOpinion };
          this.editIndex = null; // Resetea el índice de edición
        } else {
          // Agrega una nueva opinión
          this.opinions.push({ ...this.newOpinion });
        }

        // Limpia los inputs
        this.newOpinion.name = '';
        this.newOpinion.comment = '';
      },
      editOpinion(index) {
        // Pone la opinión seleccionada en los inputs para editar
        this.newOpinion = { ...this.opinions[index] };
        this.editIndex = index; // Guarda el índice de edición
      },
      deleteOpinion(index) {
        // Elimina la opinión de la lista
        this.opinions.splice(index, 1);
        // Resetea el índice de edición si está editando la misma opinión que eliminó
        if (this.editIndex === index) {
          this.editIndex = null;
          this.newOpinion.name = '';
          this.newOpinion.comment = '';
        }
      }
    }
  };
  </script>

  <style scoped>
  .App {
    max-width: 600px;
    margin: 0 auto;
    padding: 20px;
    font-family: Arial, sans-serif;
    color: #333;
  }

  h1 {
    text-align: center;
    color: #2c3e50;
  }

  .game-img {
    width: 100%;
    height: auto;
    border-radius: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    margin-bottom: 20px;
  }

  .opinion-form {
    display: flex;
    flex-direction: column;
    gap: 15px;
    margin-bottom: 30px;
  }

  .input-field,
  .textarea-field {
    width: 100%;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
    box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.1);
    font-size: 16px;
  }

  .input-field:focus,
  .textarea-field:focus {
    outline: none;
    border-color: #2980b9;
  }

  .textarea-field {
    height: 80px;
    resize: none;
  }

  .submit-btn {
    padding: 10px 15px;
    background-color: #2980b9;
    color: #fff;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }

  .submit-btn:hover {
    background-color: #1e6f9f;
  }

  .opinions-list {
    margin-top: 30px;
  }

  .opinion-card {
    border: 1px solid #ddd;
    border-radius: 8px;
    padding: 15px;
    margin-bottom: 15px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    transition: transform 0.2s ease;
  }

  .opinion-card:hover {
    transform: translateY(-2px);
  }

  .opinion-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .opinion-header h3 {
    margin: 0;
    color: #2980b9;
  }

  .opinion-actions {
    display: flex;
    gap: 10px;
  }

  .edit-btn,
  .delete-btn {
    padding: 5px 10px;
    font-size: 14px;
    cursor: pointer;
    border: none;
    border-radius: 5px;
    transition: background-color 0.3s ease;
  }

  .edit-btn {
    background-color: #f39c12;
    color: #fff;
  }

  .edit-btn:hover {
    background-color: #e08e0b;
  }

  .delete-btn {
    background-color: #e74c3c;
    color: #fff;
  }

  .delete-btn:hover {
    background-color: #c0392b;
  }
  </style>