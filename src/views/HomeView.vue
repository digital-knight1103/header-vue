<template>
  <div class="wrapper">
    <div class="search">
      <label for="search">
        Szukaj
        <input
          id="search"
          name='search'
          type="text"
          v-model="searchValue"
          @input='handleInput'>
      </label>
      <ul>
        <li v-for='item in results' :key="item.data[0].nasa_id">
          <p>Info: {{ item.data[0].description }}</p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
/* eslint-disable */
import axios from 'axios';
import debounce from 'lodash.debounce';

const URL = 'https://images-api.nasa.gov/search';

export default {
  name: 'HomeView',
  data() {
    return {
      searchValue: '',
      results: [],
    };
  }, 
  /*  inportujemy bibliotekę axios do pracy z zewnętrzynum api 
  oraz część Lodash która zarządza nam aby nie wysyłac za często zapytań do serwera
  wiec po wpisywaniu w input zapytanie zostanie wysłane po czasie 
  aby nie generować zbędnych zapytań po każdym kliknięciu przycisku */
  methods: {
    handleInput: debounce(function() {
      axios.get(`${URL}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          console.log(response.data.collection.items);
        })
        .catch((error) => {
          console.log(error);
        });
    }, 500),
  },
};
</script>

<style lang='scss' scoped>
.wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
  margin: 0;
  padding: 30px;
}
.search {
  width: 300px;
  display: flex;
  flex-direction: column;

  label {
    font-family: Montserrat, sans-serif;
  }
  input {
    height: 30px;
    border-bottom-width: 1px solid block;
  }
  p {
    color: red;
  }
}
</style>
