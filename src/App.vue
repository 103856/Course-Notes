<script setup>
import { ref } from "vue";

const showmodal = ref(false);
const newNote = ref("");
const notes = ref([]);

function getRandomColor() {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
}

const addNote = () => {
  notes.value.push({
    id: Math.floor(Math.random() * 1000000),
    text: newNote.value,
    date: new Date(),
    backgroundColor: getRandomColor(),
  });
  showmodal.value = false;
};
</script>

<template>
  <main>
    <div v-if="showmodal" class="overlay">
      <div class="modal">
        <textarea
          v-model="newNote"
          name="note"
          id="note"
          cols="30"
          rows="10"
        ></textarea>
        <button @click="addNote">Add Note</button>
        <button class="close" @click="showmodal = false">Close</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showmodal = true">+</button>
      </header>
      <div class="cards-container">
        <div
          v-for="note in notes"
          :key="note.id"
          class="card"
          :style="{ backgroundColor: note.backgroundColor }"
        >
          <p class="main-text">{{ note.text }}</p>
          <p class="date">{{ note.date.toLocaleDateString("en-US") }}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<style>
main {
 
  height: 100vh;
  width: 100vw;
  background-image: url("./components/imagenes/5c1cb58b41c7d-wallpaper-preview.png"); /* Ruta relativa a la imagen */
  background-size: cover; /* Ajusta la imagen para cubrir todo el fondo */
  background-repeat: no-repeat; /* Evita que la imagen se repita */
  background-position: center; /* Centra la imagen */
  background-color: rgba(0, 0, 0, 0.5); /* Capa negra semitransparente */
  background-blend-mode: darken; 
}
.container {
  max-width: 90%;
  padding: 10px;
  margin: 0 auto;
}
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
h1 {
  border: 5px solid black !important;
  font-weight: bold;
  margin-bottom: 25px;
  font-size: 75px;
  background-color: rgb(240, 240, 231); 
  display: inline-block; 
  padding: 5px 10px; 
  border-radius: 15px; 
}
header button {
  border: 5px solid black !important;
  border: none;
  padding: 10px;
  width: 50px;
  height: 50px;
  cursor: pointer;
  background-color: rgb(255, 255, 255);
  border-radius: 15%;
  color: rgb(0, 0, 0);
  font-size: 20px;
}
.card {
  width: 225px;
  height: 225px;
  background-color: rgb(237, 182, 44); /* Color de fondo */
  padding: 15px;
  border-radius: 15px; /* Bordes redondeados */
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  margin-right: 20px;
  margin-bottom: 20px;
  box-shadow: 0px 10px 20px rgba(0, 0, 0, 0.3), 0px 4px 10px rgba(0, 0, 0, 0.2);
  overflow: hidden;
  transition: transform 0.2s ease, box-shadow 0.2s ease; 
}
.card:hover {
  transform: translateY(-5px); 
  box-shadow: 0px 8px 15px rgba(0, 0, 0, 0.2); 
}
.main-text {
  font-size: 18px;
  font-weight: bold;
  text-align: center;
  color: #333; 
  word-wrap: break-word; 
  overflow-wrap: break-word; 
  text-overflow: ellipsis;
}
textarea {
  width: 100%;
  height: 100%; 
  resize: none; 
  overflow-y: auto; 
  padding: 10px;
  border-radius: 10px;
  font-size: 16px;
}

.date {
  font-size: 14px;
  font-weight: 500;
  color: #666; 
}
.cards-container {
  display: flex;
  flex-wrap: wrap;
}
.overlay {
  position: fixed; 
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.77); 
  z-index: 10;
  display: flex; 
  justify-content: center; 
  align-items: center; 
}
.modal {
  width: 750px;
  background-color: white;
  border-radius: 10px;
  padding: 30px;
  position: relative;
  display: flex;
  flex-direction: column;
}
.modal button {
  padding: 10px 20px;
  font-size: 20px;
  width: 100%;
  background-color: blueviolet;
  border: none;
  color: white;
  cursor: pointer;
  margin-top: 15px;
}
.modal .close {
  background: rgb(193, 15, 15);
  margin-top: 7px;
}
</style>
