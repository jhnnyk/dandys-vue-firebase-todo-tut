<script setup>
import { ref, onMounted } from 'vue'
import { v4 as uuidv4 } from 'uuid'
import { collection, getDocs } from 'firebase/firestore'
import { db } from '@/firebase'

const todos = ref([
  // { id: 'id1', content: 'Shave my head', done: false },
  // { id: 'id2', content: 'Take a shower', done: true },
  // { id: 'id3', content: 'Buy milk', done: false },
])

onMounted(async () => {
  const querySnapshot = await getDocs(collection(db, 'todos'))
  let fbTodos = []
  querySnapshot.forEach((doc) => {
    const todo = {
      id: doc.id,
      content: doc.data().content,
      done: doc.data().done,
    }
    fbTodos.push(todo)
  })
  todos.value = fbTodos
})

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

const deleteTodo = (id) => {
  todos.value = todos.value.filter((todo) => todo.id !== id)
}

const toggleDone = (id) => {
  const index = todos.value.findIndex((todo) => todo.id === id)
  todos.value[index].done = !todos.value[index].done
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

    <div class="card" :class="{ 'has-background-success-light': todo.done }" v-for="todo in todos">
      <div class="card-content">
        <div class="content">
          <div class="columns is-mobile is-vcentered">
            <div class="column" :class="{ 'has-text-success line-through': todo.done }">
              {{ todo.content }}
            </div>
            <div class="column is-5 has-text-right">
              <button
                class="button"
                :class="todo.done ? 'is-success' : 'is-light'"
                @click="toggleDone(todo.id)"
              >
                &check;
              </button>
              <button @click="deleteTodo(todo.id)" class="button is-danger ml-2">&cross;</button>
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

.line-through {
  text-decoration: line-through;
}
</style>
