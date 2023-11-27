<template>
  <div v-for="city in savedCities" :key="city.id">
    <CityCard :city="city" @click="gotoCityView(city)" />
  </div>
</template>

<script setup>
import axios, { all } from 'axios';
import { ref } from 'vue';
import { useRouter } from 'vue-router';
import CityCard from './CityCard.vue';

const apiKey = '7efa332cf48aeb9d2d391a51027f1a71';

const savedCities = ref([]);
const getCities = async () => {
  if (localStorage.getItem('savedCities')) {
    savedCities.value = JSON.parse(localStorage.getItem("savedCities"));
    const requests = [];
    savedCities.value.forEach((city) => {
      requests.push(axios.get(
        `https://api.openweathermap.org/data/2.5/weather?lat=${city.coords.lat}&lon=${city.coords.lng}&appid=${apiKey}&units=metric`
      ));
    });

    const weatherData = await Promise.all(requests);

    weatherData.forEach((value, index) => {
      console.log(value.data);
      savedCities.value[index].weather = value.data;
    });
  }

}
const router = useRouter();
const gotoCityView = (city) => {
  router.push({
    name: "city.view",
    params: { state: city.state, city: city.city },
    query: { lat: city.coords.lat, lng: city.coords.lng }
  });
  // console.log('akjhdash');
}
await getCities();


</script>