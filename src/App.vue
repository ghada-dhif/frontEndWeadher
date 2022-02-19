<template>
  <div id="app">
    <router-view />
  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      api_key: '37777278fbmshab9a1fbeec341d4p1db450jsn7a25b4235e3b',
      url_base: 'https://weatherapi-com.p.rapidapi.com/current.json'
    }
  }
}
</script>
