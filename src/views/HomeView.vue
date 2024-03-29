<template>
  <main class="container text-white">
    <div class="pt-4  relative">
      <input
        type="text"
        placeholder="Search here"
        class="py-2 px-1 w-full bg-transparent border-b focus:border-weather-primary focus:outline-none focus:shadow-md"
        v-model="searchTerm.query"
        @input="handleSearch()"
      />
      <!-- <button class="button1" @click="handleSearch">Search</button> -->
    </div>
    <div class="bg-white my-2 rounded-lg shadow-lg" id="bg">
      <!-- <div v-for="place in searchTerm.results" :key="place.id">
        <button @click="getWeather(place.id)" class="px-3 my-2 hover:font-bold w-full text-left" >
            {{ place.name }}, {{ place.region }}, {{ place.country }}
        </button>
      </div> -->
      <ul>
        <li v-for="place in searchTerm.results" :key="place.id" 
        class="py-2 cursor-pointer" @click="getWeather(place.id)">
        {{ place.name }}, {{ place.region }}, {{ place.country }}
        </li>
      </ul>
    </div>
  </main>
</template>

<script setup>
import { reactive, ref } from "vue";

const emit = defineEmits(['place-data'])

const searchTerm = reactive({
  query: "",
  timeout: null,
  results: null,
});

const handleSearch = () => {
  clearTimeout(searchTerm.timeout);
  searchTerm.timeout = setTimeout(async () => {
    if (searchTerm.query !== ''){
      const res = await fetch(`http://api.weatherapi.com/v1/search.json?key=958c91f7e9f64023bf0124044242103&q=${searchTerm.query}`);

    const data = await res.json()
    searchTerm.results = data

    } else{
      searchTerm.results = null
    }
  
  }, 500);
}

const getWeather = async (id) => {
  const res = await fetch(`http://api.weatherapi.com/v1/forecast.json?key=958c91f7e9f64023bf0124044242103&q=id:${id}&days=3&aqi=no&alerts=no`)
const data = await res.json()
emit('place-data',data)

console.log(data)
}


</script>

<style>

.button1 {
  background-color: #04AA6D;
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
}
#bg{
  background-color: lightblue;
}
</style>

