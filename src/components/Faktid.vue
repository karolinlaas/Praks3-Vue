<template>
  <div>
    <h1>Faktid numbrite kohta</h1>
    <p>Huvitavad faktid iga numbri kohta</p>
    <input type="number" v-model="number">
    <input type="number" v-model="increment" min='0'>
    <ul v-cloak v-for="">
      <li v-for="(item, index) in data" v-bind:key="index">{{ item }}</li>
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
      increment: 0,
      items: []
    }
  },
  watch: {
    number() {
      this.getFacts()
    },
    increment() {
      this.getFacts()
    }
  },
  methods: {
    getFacts () {
      if (this.number !== '' && this.inc !== '') {
        let url = `http://numbersapi.com/${this.number}..${parseInt(this.increment) + parseInt(this.number)}`

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
    margin-top: 25vh;
  }
  [v-cloak] {
    display: none;
  }
  input {
    margin-left: 10px;
    margin-right: 10px;
    padding: 5px;
  }
</style>
