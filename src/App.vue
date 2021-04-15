<template>
  <div id="app">
    <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
    <header>
      <h1>Input Gallery</h1>
      <p>Choose your input field or create one yourself</p>
    </header>
    <main>
      <div>
        <InputComp />
      </div>
      <div>
        <!-- <InputComp class="md"/> -->
      </div>
    </main>
  </div>
</template>

<script>
import InputComp from './components/InputComp.vue'

export default {
  name: 'App',
  components: {
    InputComp
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  padding: 10px;
}

.md input{
  height: 2em;
}

header {
  margin-bottom: 15px;
}
</style>
