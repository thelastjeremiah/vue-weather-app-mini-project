<template>
  <div class="flex justify-center items-center h-screen bg-main">
    <div class="bg-[#191b1c77] p-6 rounded-md mx-5">
      <form v-on:submit.prevent="getWeather" class="flex justify-center items-center">
        <input type="text" v-model="city" placeholder="Enter a city name" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline placeholder:Poppins-font">
        <button type="submit" class="bg-[#fcfcfcf8] rounded-full p-1.5 mx-4">
          <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6 text-orange-700 ">
            <path stroke-linecap="round" stroke-linejoin="round" d="M21 21l-5.197-5.197m0 0A7.5 7.5 0 105.196 5.196a7.5 7.5 0 0010.607 10.607z" />
          </svg>
        </button>
      </form>
      <div v-if="loading">
        <div class="flex justify-center items-center mx-10">
          <div class="inline-block animate-spin rounded-full h-16 w-16 border-t-2 border-b-2 border-rose-700 mt-10 "></div> 
        </div>
      </div>
      <div v-if="weatherData">
        <div class="mx-5">
          <p class="text-white font-medium Poppins-font mt-3">{{ weatherData.name }}, {{ weatherData.sys.country }}</p>
          <div class="flex">
            <p class="text-white font-medium Poppins-font mt-3">{{ weatherData.weather[0].main }}</p>
            <img :src="'http://openweathermap.org/img/wn/' + weatherData.weather[0].icon + '.png'" />
          </div>
          <p class="text-white font-medium Poppins-font mt-3">{{ weatherData.main.temp }}°C</p>
          <p class="text-white font-medium Poppins-font mt-3">{{ weatherData.main.humidity }}% humidity</p>
          <p class="text-white font-medium Poppins-font mt-3">{{ weatherData.wind.speed }} km/h wind speed</p>
        </div>
      </div>
      <div v-if="errorMsg" class="flex justify-center my-10">
        <span class="text-white font-medium Poppins-font uppercase">{{ errorMsg }}</span>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      city: '',
      weatherData: null,
      loading: false,
      errorMsg: '',
      apiKey: 'c384af62bf62e7da49977b4b06e78b85'
    }
  },
  methods: {
    async getWeather() {
      this.loading = true;
      this.errorMsg = ''
      const apiUrl = `https://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=${this.apiKey}&units=metric`;
      try {
        const response = await axios.get(apiUrl);
        this.weatherData = response.data;
        console.log(this.weatherData)
      } catch (error) {
        console.log(error);
        this.errorMsg = 'this city does not exist in our database';
        this.weatherData = null;
      } finally {
        this.loading = false;
      }
    }
  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap');

.bg-main{
  background-image: url('@/assets/main-bg.jpg');
}

.Poppins-font{
  font-family: 'Poppins', sans-serif;
}

</style>
