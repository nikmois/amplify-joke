<template>
  <div class="dad-joke-container">
    <h2 class="title">🤣 Get a Random Joke 🤣</h2>
    <div class="input-container">
      <button @click="getRandomJoke" class="button" :disabled="isLoading">
        <span v-if="isLoading">Loading...</span>
        <span v-else>Get Joke</span>
      </button>
    </div>
    <div v-if="joke" class="dad-joke-result">
      <p class="joke-text">{{ joke.setup }}</p>
      <p class="joke-text">{{ joke.punchline }}</p>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      topic: '',
      joke: null,
      isLoading: false
    }
  },
  methods: {
    async getRandomJoke() {
      this.isLoading = true
      this.joke = null
      try {
        const response = await axios.get('https://official-joke-api.appspot.com/random_joke')

        console.log(response.data)
        this.joke = response.data
      } catch (error) {
        console.error('Error fetching joke:', error)
        this.joke = 'Error fetching joke'
      } finally {
        this.isLoading = false
      }
    }
  }
}
</script>

<style scoped>
.dad-joke-container {
  text-align: center;
  margin: 20px;
  padding: 20px;
  border: 2px solid #ff6f61;
  border-radius: 10px;
  background-color: #ffecb3;
}

.title {
  font-size: 2em;
  margin-bottom: 20px;
  color: #ff6f61;
}

.input-container {
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
}

.input {
  padding: 10px;
  border-radius: 5px;
  border: 2px solid #ff6f61;
  margin-right: 10px;
}

.button {
  padding: 10px 20px;
  border-radius: 5px;
  background-color: #ff6f61;
  color: #fff;
  border: none;
  cursor: pointer;
}

.dad-joke-result {
  margin-top: 20px;
  font-size: 1.5em;
  color: #ff6f61;
  background-color: #fff;
  padding: 10px;
  border-radius: 5px;
  border: 2px solid #ff6f61;
}

.joke-text {
  margin: 0;
}

.button {
  position: relative;
}

.button span {
  visibility: visible;
}

.button span.loader {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  visibility: hidden;
}
</style>
