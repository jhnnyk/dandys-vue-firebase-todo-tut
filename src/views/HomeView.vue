<script setup>
import { ref } from 'vue'

const todos = ref([
  { id: 'id1', content: 'Shave my head', done: false },
  { id: 'id2', content: 'Take a shower', done: false },
  { id: 'id3', content: 'Buy milk', done: false },
])
</script>

<template>
  <main>
    <h1 class="is-size-1 has-text-centered">Badass Todo</h1>

    <div class="field is-grouped mb-5">
      <p class="control is-expanded">
        <input type="text" class="input" placeholder="Add a todo" />
      </p>
      <p class="control">
        <a href="#" class="button is-info">Add</a>
      </p>
    </div>

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
