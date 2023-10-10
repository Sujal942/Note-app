<script setup>
import { ref } from "vue";

const showModel = ref(false);
const newNote = ref("");
const notes = ref([]);

function clickChangeBg() {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
}

const addNotes = () => {
  notes.value.push({
    id: Math.floor(Math.random() * 1000000),
    text: newNote.value,
    date: new Date(),
    backgroundColor: clickChangeBg(),
  });
  showModel.value = false;
  newNote.value = "";
};
</script>


<template>
  <main>
    <div v-if="showModel" class="overlay">
      <div class="model">
        <textarea
          v-model="newNote"
          name="note"
          id="note"
          cols="30"
          rows="10"
        ></textarea>
        <button @click="addNotes">Add Notes</button>
        <button class="close" @click="showModel = false">Close</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showModel = true">+</button>
      </header>
      <div class="card-container">
        <div
          v-for="note in notes"
          :key="note.id"
          class="card"
          :style="{ backgroundColor: note.backgroundColor }"
        >
          <p class="text">
            {{ note.text }}
          </p>
          <p class="date">{{ note.date.toLocaleDateString("en-US") }}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {};
</script>

<style scoped>
main {
  height: 100vh;
  width: 100vw;
}
.overlay {
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.346);
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: center;
}
.model {
  width: 600px;
  height: 400px;
  border-radius: 20px;
  padding: 10px;
  position: relative;
  display: flex;
  justify-content: center;
  flex-direction: column;
}
.model button {
  cursor: pointer;
  padding: 8px 20px;
  margin: 5px 0;
  width: 100%;
  background-color: blue;
  color: white;
  font-size: larger;
  border: none;
  border-radius: 5px;
}

.model .close {
  background-color: red;
}
.container {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}
header {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 250px;
  margin-top: 50px;
}
header > h1 {
  text-shadow: 2px 2px 5px 2px gold;
  font-size: 40px;
  letter-spacing: 10px;
}
header > h1:hover {
  text-decoration: underline;
}
header > button {
  padding: 10px 20px;
  cursor: pointer;
  font-size: 30px;
  background-color: rgb(208, 198, 198);
  box-shadow: 2px 2px 6px 2px silver;
  border-radius: 30px;
  border: none;
}
header > button:hover {
  background-color: aliceblue;
  color: blueviolet;
  transition: all ease-in cubic-bezier(0.445, 0.05, 0.55, 0.95);
}
.card {
  height: 250px;
  width: 250px;
  padding: 20px;
  border-radius: 20px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-right: 20px;
  margin-left: 20px;
  margin-bottom: 35px;
  margin-top: 40px;
}
.card-container {
  height: 600px;
  width: 70%;
  margin-top: 20px;
  border-radius: 20px;
  box-shadow: 1px 1px 5px 3px rgba(152, 143, 143, 0.232);
  display: flex;
  justify-content: center;
  overflow: hidden;
  overflow-y: scroll;
  flex-wrap: wrap;
}
.card-container::-webkit-scrollbar {
  scroll-behavior: smooth;
  overflow: hidden;
}
.card p {
  color: brown;
}
.date {
  font-size: 10px;
  font-weight: 900;
  letter-spacing: 10px;
}
</style>