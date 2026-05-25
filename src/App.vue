<script setup lang="ts">
import Certificates from './sections/Certificates.vue';
import Experience from './sections/Experience.vue';
import Skills from './sections/Skills.vue';
import About from './sections/About.vue';
</script>

<template>
<v-app>
    <v-main>
      <v-container>
        <About />
        <Skills />
        <Certificates />
        <Experience />
      </v-container>
    </v-main>
  </v-app>
</template>

<style>
* {
  font-family: 'Fira Code', monospace;
}
.ascii-container {
  width: 100%;
  display: flex;
  justify-content: center;
  overflow-x: auto; 
  padding: 20px 0;
}

.ascii-text {
  color: #00ff66;
  text-shadow: 0 0 8px rgba(0, 255, 102, 0.65);
  font-size: 0.6vw;
  line-height: 1.0; 
  letter-spacing: -0.05em; 
  white-space: pre;
}

@media (max-width: 768px) {
    .ascii-text {
        font-size: 2.5vw;
    }
}
</style>
