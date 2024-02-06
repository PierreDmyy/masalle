<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <div>
    <header>
      <img class="logo" src="@/assets/logoCFP02.png"></img>
      <h1 class="title">Localiser ma salle :</h1>
    </header>
    <HelloWorld />
  </div>
</template>

<style scoped>
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
    justify-content: flex-end; /* Pour aligner les éléments à droite */
    align-items: center; /* Pour centrer verticalement les éléments */
  }

  .logo {
    height: 100px;
    width: auto;
    margin-right: auto; /* Pour pousser le titre à droite */
  }

  .title {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    margin: 0; /* Supprimer les marges par défaut */  }

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

