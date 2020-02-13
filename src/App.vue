<template>
  <div id="app">
    <h1>{{ location }}</h1>
    <Input @submit="setLocation" />
  </div>
</template>

<script>
import Input from './components/Input.vue'

export default {
  name: 'App',
  data() {
    return {
      location: '',
    }
  },
  methods: {
    setLocation(text) {
      this.location = text
    }
  },
  components: {
    Input,
  },
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
}
</style>
