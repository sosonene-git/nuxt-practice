<script setup lang="ts">
defineProps<{
  count: number
}>()
</script>

<template>
  <div class="stats">
    <span>あと {{ count }} つのタスク</span>
  </div>
</template>

<style scoped>
.stats {
  font-size: 0.9rem;
  color: #636e72;
  margin-bottom: 1rem;
  padding-bottom: 1rem;
  border-bottom: 1px solid #f0f0f0;
}
</style>
