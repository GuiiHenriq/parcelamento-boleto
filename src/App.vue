<template>
  <div id="app">
    <h1 class="title">Parcelamento Boleto</h1>
    <Parcelado />
  </div>
</template>

<script>
import Parcelado from './components/Parcelado.vue'

export default {
  name: 'App',
  components: {
    Parcelado
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Baloo+Paaji+2&display=swap');

* {
  box-sizing: border-box;
}

body,
ul,
li,
h1,
h2,
p {
  padding: 0px;
  margin: 0px;
}

ul {
  list-style: none;
}

body {
  font-family: 'Baloo Paaji 2', cursive;
  color: #345;
  background: url("./assets/pattern.svg") repeat top;
}

a {
  color: #345;
  text-decoration: none;
}

h1, p {
  text-align: center;
}

#app {
  display: flex;
  min-height: 100vh;
  flex-direction: column;
}

label {
  margin-bottom: 5px;
}

input,
footer {
  border-radius: 4px;
  border: 1px solid white;
  padding: 15px;
  box-shadow: 0 4px 8px rgba(30, 60, 90, 0.1);
  transition: all 0.3s;
  font-size: 1rem;
  font-family: 'Baloo Paaji 2', cursive;
  margin-bottom: 15px;
}

input:hover,
input:focus {
  outline: none;
  box-shadow: 0 6px 12px rgba(30, 60, 90, 0.2);
  border-color: #87f;
}

.title {color: #1abc9c}
</style>
