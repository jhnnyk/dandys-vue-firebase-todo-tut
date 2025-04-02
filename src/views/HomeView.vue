<script setup></script>

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

    <div class="card" v-for="i in 3">
      <div class="card-content">
        <div class="content">
          <div class="columns is-mobile is-vcentered">
            <div class="column">Shave my head</div>
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
