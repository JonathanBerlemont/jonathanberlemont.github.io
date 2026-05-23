<script lang="ts" setup>
import Greeblies from '@/components/Greeblies.vue';
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
            <p>6+ years building web applications — starting at Deloitte on LMS platforms, then 5 years at Sciensano developing healthcare software in a small team on increasingly complex systems.</p>
            <p>It was at Sciensano that I developed a real interest in quality engineering: as the codebase and infrastructure grew, the need for proper monitoring, quality gates, and structured testing became impossible to ignore. I found myself drawn to that problem more than the development itself.</p>
            <p>Having worked on the development side, I understand how bugs are introduced, not just where to find them — which I believe makes me a stronger QA engineer than someone who hasn't.</p>
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
