<template>
  <div>
    <h1>Numbrifaktid</h1>
    <h3>Sisesta numbrid, et näha fakte!</h3>
    <input type="number" min="0" v-model="number">
    <p v-cloak>{{ data }}</p>
  </div>
</template>

<script>
const axios = require('axios')

export default {
  name: 'Faktid',
  data () {
    return {
      data: '',
      number: 0
    }
  },
  watch: {
    number () {
      if (this.number !== '') {
        let url = `http://numbersapi.com/${this.number}`
        axios.get(url)
          .then(response => {
            this.data = response.data
          })
          .catch(error => {
            console.log(error)
          })
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    div {
        text-align: center;
    }
    [v-cloak] {
        display: none;
    }
</style>
