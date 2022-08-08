<script setup lang="ts">
import { defineProps, defineEmits, PropType } from 'vue';

defineProps({
  completeList: {
    type: Object as PropType<string[]>,
    required: true,
  },
});

defineEmits<{ (e: 'back', idx: number): void }>();
</script>

<template>
  <li v-for="(completeTodo, i) in completeList">
    <div>
      <span>{{ completeTodo }}</span>
      <button @click="$emit('back', i)">戻す</button>
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
