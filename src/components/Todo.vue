<script setup lang="ts">
import { ref, reactive } from 'vue';
import IncompleteTodo from './IncompleteTodo.vue';
import CompleteTodo from './CompleteTodo.vue';

interface Todo {
  todoList: string[],
  completeList: string[],
}

const errMsg = ref<string | null>(null);
const newTodo = ref<string>('');
const todo = reactive<Todo>({
  todoList: [],
  completeList: [],
});

const addTodo = () => {
  if (!newTodo.value) {
    errMsg.value = '入力してください！'
    return;
  } else {
    errMsg.value = null;
  }
  todo.todoList.push(newTodo.value);
  newTodo.value = '';
};

const deleteTodo = (index: number) => {
  todo.todoList.splice(index, 1);
};
const addCompleteList = (index: number) => {
  todo.completeList.push(todo.todoList[index]);
  todo.todoList.splice(index, 1);
};

const backTodo = (index: number) => {
  todo.todoList.push(todo.completeList[index]);
  todo.completeList.splice(index, 1);
};
</script>

<template>
  <template v-if="errMsg">
    <div class="err">
      <span>{{ errMsg }}</span>
    </div>
  </template>
  <div class="card">
    <input type="text" placeholder="TODOを入力" v-model="newTodo" />
    <button id="add-btn" @click="addTodo">追加</button>
  </div>
  <div class="card d-col">
    <h2>未完了のTODO</h2>
    <ul>
      <IncompleteTodo
        :incomplete-todos="todo.todoList"
        @complete="addCompleteList"
        @delete="deleteTodo"
      />
    </ul>
  </div>
  <div class="card d-col">
    <h2>完了したTODO</h2>
    <ul>
      <CompleteTodo :complete-list="todo.completeList" @back="backTodo" />
    </ul>
  </div>
</template>

<style scoped>
.card {
  padding: 2em;
  display: flex;
  justify-content: center;
  align-items: center;
}

input {
  margin: 1.5rem;
  border-radius: 8px;
  border: none;
  padding: 8px 16px;
  outline: none;
}

h2 {
  color: #a3a3a3;
}

ul {
  margin-bottom: 1rem;
}

li {
  margin: 1rem auto;
}

.err {
  background-color: #f5b2ac;
  height: 100px;
  border-radius: 0.25rem;
  font-size: 36px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
}

.d-col {
  flex-direction: column;
}
</style>
