<script lang="ts" setup>
import certificates from '@/data/certificates.json';
</script>

<template>
    <h2 class="ascii-container">
        <pre class="ascii-text">
   _____          _   _  __ _           _   _                 
  / ____|        | | (_)/ _(_)         | | (_)                
 | |     ___ _ __| |_ _| |_ _  ___ __ _| |_ _  ___  _ __  ___ 
 | |    / _ \ '__| __| |  _| |/ __/ _` | __| |/ _ \| '_ \/ __|
 | |___|  __/ |  | |_| | | | | (_| (_| | |_| | (_) | | | \__ \
  \_____\___|_|   \__|_|_| |_|\___\__,_|\__|_|\___/|_| |_|___/
        </pre>
    </h2>
    <div class="certificates">
        <v-card
            v-for="certificate in certificates"
            :key="certificate.name"
            :title="certificate.name"
            variant="outlined"
            color="#00ff66"
        >
            <template #prepend>
                <img :src="`/logos/${certificate.logo}`" style="width: 50px; height: 50px; object-fit: contain;" />
            </template>
            <template #append v-if="certificate.url.length > 0">
                <a :href="certificate.url" target="_blank" rel="noopener noreferrer">
                    <v-icon icon="mdi-open-in-new" color="#00ff66" />
                </a>
            </template>
            <template #append v-else>
                <small>Soon</small>
                <v-icon icon="mdi-loading" class="spinning" color="#00ff66" />
            </template>
        </v-card>
    </div>
</template>

<style scoped>
.certificates {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 20px;
    .v-card:deep(.v-card-title) {
        white-space: normal;
        word-break: break-word;
    }
}
.spinning {
    animation: spin 1s linear infinite;
}

@keyframes spin {
    from { transform: rotate(0deg); }
    to { transform: rotate(360deg); }
}
</style>