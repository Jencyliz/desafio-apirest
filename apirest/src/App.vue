<template>
  <div id="app">
    <ChatApp /> 
  </div>
</template>

<script>
//ChatApp
import ChatApp from '../src/components/ChatApp.vue';

export default {
  name: 'App',
  components: {
    ChatApp, 
  },
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


body{
  background-color: black;
}
</style>
