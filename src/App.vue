<script setup>
import { ref } from 'vue';
// Importem el component pont que conté el <canvas> de Phaser
import PhaserCanvas from './components/PhaserCanvas.vue';

// Variable reactiva que guarda el nom escrit a la caixa de text
const nom = ref('Anna');
// Booleà per muntar/desmuntar el joc i verificar onMounted / onUnmounted
const mostrarJoc = ref(true);
const color = ref('#10b981');
const estat = ref('Disponible');
const pausat = ref(false);

</script>

<template>
  <main class="contenidor-app">
    <!-- Tota la interfície d'usuari (inputs, botons) es fa en HTML/CSS dins de Vue -->
    <div class="controls">
      <input v-model="nom" placeholder="Escriu el teu nom d'usuari..." />
      <input type="color" v-model="color" />

      <select v-model="estat">
        <option>Disponible</option>
        <option>Ocupat</option>
        <option>Absent</option>
      </select>

       <button @click="pausat = !pausat" :disabled="!mostrarJoc">
        {{ pausat ? 'Reprèn' : 'Pausa' }}
      </button>

      <button @click="mostrarJoc = !mostrarJoc">
        {{ mostrarJoc ? 'Amaga el llenç' : 'Mostra el llenç' }}
      </button>
    </div>

    <!-- Passem 'nom' cap avall amb :nomUsuari i controlem el cicle amb v-if -->
    <PhaserCanvas v-if="mostrarJoc" :nomUsuari="nom" :colorAvatar="color" :estat="estat" :pausat="pausat"/>
  </main>
</template>
