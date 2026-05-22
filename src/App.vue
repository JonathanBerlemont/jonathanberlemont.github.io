<script setup lang="ts">
import Certificates from './sections/certificates.vue';
import Experience from './sections/experience.vue';
import Skills from './sections/skills.vue';
import About from './sections/about.vue';
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
  font-size: 0.60vw;
  line-height: 1.0; 
  letter-spacing: -0.05em; 
  white-space: pre;
}
</style>
