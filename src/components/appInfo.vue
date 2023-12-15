<template>
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
</template>

<script>
export default {
  name: 'App',
  props: {
    errorMsg: String,
    weatherData: Object,
  },
}
</script>
