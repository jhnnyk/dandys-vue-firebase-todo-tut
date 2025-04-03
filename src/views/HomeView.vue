<script setup>
import { ref } from 'vue'
import { v4 as uuidv4 } from 'uuid'

const todos = ref([
  { id: 'id1', content: 'Shave my head', done: false },
  { id: 'id2', content: 'Take a shower', done: false },
  { id: 'id3', content: 'Buy milk', done: false },
])

const newTodoContent = ref('')

const addTodo = () => {
  const newTodo = {
    id: uuidv4(),
    content: newTodoContent.value,
    done: false,
  }
  todos.value.unshift(newTodo)
  newTodoContent.value = ''
}
</script>

<template>
  <main>
    <h1 class="is-size-1 has-text-centered">Badass Todo</h1>

    <form @submit.prevent="addTodo">
      <div class="field is-grouped mb-5">
        <p class="control is-expanded">
          <input type="text" v-model="newTodoContent" class="input" placeholder="Add a todo" />
        </p>
        <p class="control">
          <button href="#" class="button is-info" :disabled="!newTodoContent">Add</button>
        </p>
      </div>
    </form>

    <div class="card" v-for="todo in todos">
      <div class="card-content">
        <div class="content">
          <div class="columns is-mobile is-vcentered">
            <div class="column">{{ todo.content }}</div>
            <div class="column is-5 has-text-right">
              <button class="button is-light">&check;</button>
              <button class="button is-danger ml-2">&cross;</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<style>
main {
  max-width: 400px;
  padding: 20px;
  margin: 0 auto;
}
</style>
