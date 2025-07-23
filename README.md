<template>
  <p>Compteur : {{ count }}</p>
  <button @click="increment">Incrémenter</button>
  <button @click="decrease">Diminuer</button>
  <button @click="reset">Reset</button>
  <hr>
  <form action="" @submit.prevent="addMovie">
    <input type="text" placeholder="Nouveau Film" v-model="newMovie">
    <button>Ajouter</button>
  </form>
  <button @click="sortMovies">Réorganiser</button>
  <ul>
    <li v-for="movie in movies" :key="movie">
      {{ movie }} <button @click="deleteMovie(movie)">Supprimer</button>
    </li>
  </ul>
  <hr>
  <ul>
    <li>{{person.firstName}}</li>
    <li>{{person.lastName}}</li>
    <li>{{person.age}}</li>
    <button @click.prevent)="randomAge">Changer Âge</button>
  </ul>
</template>

<script setup>
import { ref } from 'vue';

const person = ref({
  firstName: 'John',
  lastName: 'Doe',
  age: 20,
})

const randomAge = () => {
  person.value.age = Math.floor(Math.random() * 100);
};

const count = ref(0);
const movies = ref ([
  'Abraham Lincoln',
  'Matrix',
  'Zabrada',
  'Brasilia',
  'The Dark Knight',
])

const deleteMovie = (movie) => {
  movies.value = movies.value.filter(m => m !== movie);
}

const addMovie = () => {
  movies.value.push(newMovie.value);
  newMovie.value = '';
}

const newMovie = ref('');

const sortMovies = () => {
  movies.value.sort();
};

const reset = () => {
  count.value = 0;
};
const increment = (event) => {
  count.value++;
};
const decrease = () => {
  count.value--;
};
</script>