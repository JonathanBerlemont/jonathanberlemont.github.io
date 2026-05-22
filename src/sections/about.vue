<script lang="ts" setup>
import Greeblies from '@/components/greeblies.vue';
</script>

<template>
    <div class="ascii-container">
        <pre class="ascii-text">
       _                   _   _                   ____            _                            _   
      | |                 | | | |                 |  _ \          | |                          | |  
      | | ___  _ __   __ _| |_| |__   __ _ _ __   | |_) | ___ _ __| | ___ _ __ ___   ___  _ __ | |_ 
  _   | |/ _ \| '_ \ / _` | __| '_ \ / _` | '_ \  |  _ < / _ \ '__| |/ _ \ '_ ` _ \ / _ \| '_ \| __|
 | |__| | (_) | | | | (_| | |_| | | | (_| | | | | | |_) |  __/ |  | |  __/ | | | | | (_) | | | | |_ 
  \____/ \___/|_| |_|\__,_|\__|_| |_|\__,_|_| |_| |____/ \___|_|  |_|\___|_| |_| |_|\___/|_| |_|\__|
        </pre>
    </div>
    <v-card variant="outlined" class="about-card">
        <div class="about">
            <p>Drupal/ PHP and JavaScript developer with over 5 years of experience in the health sector, now moving into Software QA/QC Engineering.</p>
            <p>My broad technical background allows me to work closely with developers and contribute to building robust, high-quality solutions together.</p>
        </div>
        <div class="greeblies">
            <Greeblies />
        </div>
    </v-card>
</template>

<style scoped>
.about-card {
  display: grid;
  grid-template-columns: 2fr 1fr; 
  gap: 20px; 
  padding: 20px;
}
</style>