<template>
  <div>
    <span class="text-white font-medium Poppins-font uppercase">{{ errorMsg }}</span>
  </div>
</template>
  
  
<script>
export default {
  name: 'App',
  props: {
    errorMsg: String,
  },
}
</script>
