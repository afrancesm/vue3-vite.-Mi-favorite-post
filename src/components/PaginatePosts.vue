<script setup>
defineProps(['inicio', 'fin', 'longitud']);
</script>

<template>
  <div class="btn-group" role="group" aria-label="Basic example">
    <button
      type="button"
      class="btn btn-outline-primary"
      @click="$emit('prev')"
      :disabled="inicio === 0"
    >
      Prev
    </button>

    <button
      type="button"
      class="btn btn-outline-primary"
      @click="$emit('next')"
      :disabled="fin >= longitud"
    >
      Next
    </button>
  </div>
</template>
