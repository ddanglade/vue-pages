<template>
  <div class="hello">
    <h1>Top 1000 Movies</h1>
    <button @click="fetchMovies">Fetch Top Movies</button>
    <ul>
      <li v-for="movie in movies" :key="movie.id">
        {{ movie.title }} ({{ movie.year }}) - Rating: {{ movie.rating }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      movies: [],
    };
  },
  methods: {
    async fetchMovies() {
      const url = "https://imdb-top-1000-movies-series.p.rapidapi.com/byrating";
      const options = {
        method: "POST",
        headers: {
          "x-rapidapi-key": '164c17a9b1mshc0372b4ecb335d5p154d6cjsn5d1f24a765a8',
          "x-rapidapi-host": "imdb-top-1000-movies-series.p.rapidapi.com",
          "Content-Type": "application/x-www-form-urlencoded",
        },
        body: new URLSearchParams({
          above: "8.1",
          under: "8.2",
        }),
      };

      try {
        const response = await fetch(url, options);
        if (!response.ok) {
          throw new Error(`HTTP error! Status: ${response.status}`);
        }
        const result = await response.json();
        this.movies = result;
      } catch (error) {
        console.error("Fetch error:", error);
      }
    },
  },
};
</script>

<style scoped>
button {
  padding: 10px 20px;
  font-size: 16px;
  background-color: #42b983;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

button:hover {
  background-color: #369f75;
}
</style>
