<template>
  <div id="app">
    <Header />
    <Select />
    <Quiz />
  </div>
</template>

<script>

import Header from "./components/Header";
import Select from "./components/Select";
import Quiz from "./components/Quiz";

export default {
  name: 'App',
  components: {
    Header,
    Select,
    Quiz
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
