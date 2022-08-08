<script setup lang="ts">
import { defineProps, defineEmits, PropType } from 'vue';

defineProps({
  incompleteTodos: {
    type: Object as PropType<string[]>,
    required: true,
  },
});

defineEmits<{
  (e: 'complete', idx: number): void,
  (e: 'delete', idx: number): void,
}>();
</script>

<template>
  <li v-for="(todo, i) in incompleteTodos">
    <div>
      <span>{{ todo }}</span>
      <button @click="$emit('complete', i)">完了</button>
      <button @click="$emit('delete', i)">削除</button>
    </div>
  </li>
</template>

<style scoped>
ul {
  margin-bottom: 1rem;
}

li {
  margin: 1rem auto;
}

ul > li > div> span {
  margin-right: 10px;
}
</style>
