<template>
  <div>
    <Header />
    <main>
      <Grid :games="games"></Grid>
    </main>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'IndexPage',
  data() {
    return {
      games: []
    }
  },
  beforeMount() {

    fetch('https://api.rawg.io/api/games?key='+process.env.apiKey+'&page_size=20')
    .then(response => response.json())
    .then(data => {
      
      var games = data.results
      this.games = games
      console.log(games)

    })


  },
})


</script>
