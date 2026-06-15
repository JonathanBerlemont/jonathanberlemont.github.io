<script setup lang="ts">
defineProps({
  tags: {
    type: Array,
    default: () => []
  }
})
</script>

<template>
  <div class="tags">
    <v-chip
      v-for="tag in tags"
      :key="tag"
      size="small"
      class="mt-1 mr-2 mb-1 ml-0"
    >
      {{ tag }}
    </v-chip>
  </div>
</template>

<style scoped>
.tags {
  margin-top: auto;
}
</style>