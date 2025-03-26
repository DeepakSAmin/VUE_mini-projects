<script setup>
import { ref } from "vue";
import Overlay from "./overlay.vue"; 

const showModal = ref(false);
const newNote = ref("");
const notes = ref([]);
const err = ref("");

function getRandomLightColor() {
  const r = Math.floor(Math.random() * 128) + 128;
  const g = Math.floor(Math.random() * 128) + 128;
  const b = Math.floor(Math.random() * 128) + 128;
  return `rgb(${r}, ${g}, ${b})`;
}

const addNote = () => {
  if (newNote.value.length < 10) {
    err.value = "Minimum 10 characters";
    return;
  }
  notes.value.push({
    id: Math.floor(Math.random() * 1000000000000),
    note: newNote.value,
    date: new Date(),
    backgroundColor: getRandomLightColor()
  });
  showModal.value = false;
  newNote.value = "";
  err.value = "";
};

const deleteNote = (id) => {
  notes.value = notes.value.filter(note => note.id !== id);
};
</script>

<template>
  <main>
    <Overlay :show="showModal" @close="showModal = false">
      <textarea v-model.trim="newNote" placeholder="Write a note..."></textarea>
      <p v-if="err" class="error">{{ err }}</p>
      <button @click="addNote">ADD NOTE</button>
    </Overlay>

    <div class="container">
      <header>
        <h1>NOTES</h1>
        <button @click="showModal = true">+</button>
      </header>

      <div class="cards_container">
        <div v-for="val in notes" :key="val.id" class="card" :style="{ backgroundColor: val.backgroundColor }">
          <p class="main-text">{{ val.note }}</p>
          <div class="footer">
            <p class="date">{{ val.date.toLocaleDateString("en-US") }}</p>
            <button @click="deleteNote(val.id)">DELETE</button>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
.error{
    color: #b11a21;
}
main {
    height: 100vh;
    width: 100vw;
}

.container {
    max-width: 1000px;
    padding: 10px;
    margin: 0 auto;
}

header {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

h1 {
    font-weight: bold;
    margin-bottom: 25px;
    font-size: 75px;
}

header button {
    border: none;
    padding: 10px;
    width: 50px;
    height: 50px;
    cursor: pointer;
    background-color: rgb(99, 99, 99);
    border-radius: 100%;
    color: white;
    font-size: 20px;
}

.card {
    width: 225px;
    height: 225px;
    color: black;
    padding: 10px;
    border-radius: 15px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin-right: 20px;
    margin-bottom: 20px;
}

.card .footer {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.date {
    font-size: 12px;
    font-weight: bold;
}

.cards_container {
    display: flex;
    flex-wrap: wrap;
}

.cards_container button {
    width: 70px;
    height: 25px;
    border-radius: 10px;
    background-color: #b11a21;
    border: none;
    margin-top: 0; /* Ensure the button aligns properly */
}

.overlay {
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.77);
    z-index: 10;
    display: flex;
    align-items: center;
    justify-content: center;
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
    color: #d4d4dc;
    font-size: 20px;
    width: 100%;
    border: none;
    margin-top: 15px;
    cursor: pointer;
    background-color: #393f4d;
}

.modal .close {
    background-color: #b11a21;
    margin-top: 7px;
    border: none;
}


</style>
