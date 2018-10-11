<template>
  <div>
    <h1>Numbrifaktid</h1>
    <h3>Sisesta numbrid, et näha fakte!</h3>
    <input type="number" min="0" v-model="number">
    <br>
    <input type="number" min="0" v-model="inc">
    <ul>
    <li v-cloak v-for="data in data" :key="data.index">{{ data }}</li>
    </ul>
  </div>
</template>

<script>
const axios = require('axios')

export default {
  name: 'Faktid',
  data () {
    return {
      data: {},
      number: 0,
      inc: 0
    }
  },
  watch: {
    number () {
        this.getFact()
    },
    inc () {
       this.getFact()
    }
  },
    methods: {
    getFact () {
        if (this.number !== '' && this.inc !== '') {
        let url = `${'http://numbersapi.com/'}${this.number}..${parseInt(this.number) + parseInt(this.inc)}`
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
    li {
        padding-bottom: 10px;
    }
    ul {
        text-align: left;
    }
</style>
