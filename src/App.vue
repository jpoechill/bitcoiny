<template>
  <div id="app">
    <span style="background-color: #4990E2; justify-content: center; margin: auto; text-align: center; padding: 0px 56px 14px 56px; text-decoration: none;">
      <span style="padding-bottom: -10px; text-decoration: underline solid #333;">
        ${{BTCPrice}}
      </span>
    </span>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'app',
  data: () => ({
    BTCPrice: 0
  }),
  created: function () {
    this.getBTCPrice()

    setInterval(function () {
      this.getBTCPrice()
      console.log('updated')
    }.bind(this), 1000)
  },
  methods: {
    getBTCPrice: function () {
      axios.get(`https://api.coinbase.com/v2/prices/BTC-USD/spot`)
      .then(response => {
        this.BTCPrice = Math.round(response.data.data.amount)
      })
      .catch(e => {
        this.errors.push(e)
      })
    }
  }
}
</script>

<style>

body, html {
  background-color: #fafafa;
  height: 98%;
}

#app {
  font-family: "HelveticaNeue-Light", "Helvetica Neue Light", "Helvetica Neue", Helvetica, Arial, "Lucida Grande", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  display: flex;
  align-items: center;
  color: #fff;
  width: 100%;
  height: 100%;
  font-weight: 700;
  font-size: 172px;
}
</style>
