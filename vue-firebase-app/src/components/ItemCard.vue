<template>
  <div class="col-md-4 mb-3">
    <div class="card h-100" @click="$emit('click')">
      <img :src="item.image" class="card-img-top" alt="..." />
      <div class="card-body">
        <h5 class="card-title">{{ item.title }}</h5>
        <p class="card-text">{{ item.description }}</p>
        <span class="badge bg-secondary me-1" v-for="tag in item.tags" :key="tag">{{ tag }}</span>
      </div>
    </div>
  </div>
</template>

<script setup>
defineProps(['item']);
</script>
