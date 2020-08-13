<template>
  <div id="app">
    <img class="logo" src="./assets/ghibli-logo.png" alt="Ghibli logo" />
    <p class="clear" v-if="loading">Loading...</p>
    <p class="clear" v-else-if="hasError">We cannot list Ghibli films at the moment. Sorry for the  inconvenience 😢</p>
    <div class="container" v-else>
      <button class="button reset-button" v-on:click="resetCache">Reset local cache & reload</button>
      <div class="film-list" >
        <Film v-for="film in films" :key="film.id" :film="film" />
      </div>  
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import Film from './components/Film'

export default {
  name: 'App',
  components: {
    Film,
  },
  data() {
    return {
      films: [],
      loading: true,
      hasError: false,
    }
  },
  async mounted() {
    const lastRefreshTimestamp = localStorage.getItem('timestamp') || null

    try {
      // If we still have fresh data from the local storage, we use it, 
      // otherwise we call the API 
      if (lastRefreshTimestamp !== null && lastRefreshTimestamp < Date.now() - 60) {
        this.films = JSON.parse(localStorage.getItem('films'))
      } else {
          const { data } = await axios.get(`${process.env.VUE_APP_API_URL}/films?with_people=true`)
          this.films = data.films || []
          localStorage.setItem('films', JSON.stringify(data.films))
          localStorage.setItem('timestamp', Date.now())
      }
    } catch(err) {
      this.hasError = true
    } finally {
      this.loading = false
    }
    
  },
  methods: {
    resetCache: () => {
      localStorage.removeItem('timestamp')
      localStorage.removeItem('films')
      location.reload()
    }
  }
}
</script>

<style>
html {
  height: 100%;
}

body {
  margin: 0;
  height: 100%;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: #00A8E6;
  padding: 30px 0 60px;
  min-height: 100%;
  box-sizing: border-box;
}
</style>

<style scoped>
.clear {
  color: #ffffff;
}

.container {
  width: 75%;
  margin: auto; 
  display: flex;
  flex-direction: column;
}

.button {
  background-color: #fffefa;
  border: 0;
  border-radius: 2px;
  padding: 5px 10px;
  cursor: pointer;
  color: #2c3e50;
}

.button:focus {
  outline: none;
}

.reset-button {
  margin-bottom: 20px;
  margin-left: auto;
}

.film-list {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: 1fr;
  column-gap: 30px;
  row-gap: 30px;
}

.logo {
  margin-bottom: 60px;
  max-height: 200px;
  filter: brightness(0) invert(1);
}
</style>
