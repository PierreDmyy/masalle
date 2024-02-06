<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import { ref } from 'vue';
import HelloWorld from './components/HelloWorld.vue';

const currentTime = ref('');
const currentDate = ref('');


// Mettre à jour l'heure actuelle
setInterval(() => {
  const now = new Date();
  currentDate.value = now.toLocaleDateString('fr-FR', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' });
  currentTime.value = now.toLocaleTimeString('fr-FR', { hour: '2-digit', minute: '2-digit', second: '2-digit' });
}, 1000);
</script>

<template>
  <div>
    <header>
      <img class="logo" src="@/assets/logoCFP02.png"></img>
      <p class="date">{{ currentDate }}</p> <!-- Afficher la date ici -->
      <p class="time">{{ currentTime }}</p> <!-- Afficher l'heure ici -->
    </header>
    <HelloWorld />
  </div>
</template>



<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@700&display=swap');

header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  padding: 10px;
  background-color: #fff;
  z-index: 1000;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  display: flex;
  justify-content: space-between; /* Pour aligner les éléments aux extrémités */
  align-items: center; /* Pour centrer verticalement les éléments */
}

.logo {
  height: 100px;
  width: auto;
}

.time {
  font-family: 'Poppins', sans-serif;
  margin: 20px;
  font-size: 25px;
  color: blue;
}
.date{
  font-family: 'Poppins', sans-serif;
  margin: 0;
  font-size: 25px;
  color: blue;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}
</style>


