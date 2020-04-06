<template>
  <div class="container">
    <div>
      <input class="textInput" v-model="text" @input="autoCompleteFilter"/>
      <button class="clearButton" @click="suggestionClicked('')">Clear</button>
    </div>
    <div class="suggestionBox" v-if="this.suggestions.length > 0">
      <p class="suggestion" v-for="(suggestion, i) in this.suggestions" :key="i" @click="suggestionClicked(suggestion)">{{suggestion}}</p>
    </div>

  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'HelloWorld',
  data() {
    return {
      text: '',
      suggestions: [],
      endpoint: 'https://mock-autocomplete.herokuapp.com/autocomplete?q='
    }
  },
  methods: {
    autoCompleteFilter() {
      axios
        .get(this.endpoint + this.text)
        .then(resp => this.suggestions = resp.data.data)
        .catch(error => console.log(error.response))
    },
    suggestionClicked(suggestion) {
      this.text = suggestion
      this.suggestions = []
      this.$emit('submit', this.text);
    },
  },
}
</script>

<style scoped>
  .container {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .textInput {
    padding: 0 0.5rem;
    height: 2rem;
    width: 12rem;
    outline: none;
    border-radius: 3px;
    border: 2px black solid;
  }
  .clearButton {
    height: 2.125rem;
    width: 4rem;
    background-color: #5B89E7;
    border-radius: 3px;
    border: none;
    outline: none;
    font-weight: 700;
  }
  .suggestionBox {
    position: relative;
    right: 2rem;
    width: 13rem;
    border: 1px black solid;
  }
  .suggestion {
    margin: 1rem 0.5rem;
    list-style-type: none;
    text-align: left;
    cursor: pointer;
  }
</style>
