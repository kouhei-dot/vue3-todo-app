<script setup lang="ts">
import { ref, reactive } from 'vue';
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
      <li v-for="(_todo, i) in todo.todoList">
        <div>
          <span>{{ _todo }}</span>
          <button @click="addCompleteList(i)">完了</button>
          <button @click="deleteTodo(i)">削除</button>
        </div>
      </li>
    </ul>
  </div>
  <div class="card d-col">
    <h2>完了したTODO</h2>
    <ul>
      <li v-for="(compTodo, i) in todo.completeList">
        <div>
          <span>{{ compTodo }}</span>
          <button @click="backTodo(i)">戻す</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<style scoped>
  button {
  border-radius: 8px;
  border: 1px solid transparent;
  padding: 0.6em 1.2em;
  font-size: 1em;
  font-weight: 500;
  font-family: inherit;
  background-color: #1a1a1a;
  cursor: pointer;
  transition: border-color 0.25s;
  margin-right: 8px;
}
button:hover {
  border-color: #646cff;
}
button:focus,
button:focus-visible {
  outline: 4px auto -webkit-focus-ring-color;
}

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

ul > li > div> span {
  margin-right: 10px;
}

.d-col {
  flex-direction: column;
}
</style>
