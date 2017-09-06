<template>
  <div class="container">
    <h1>{{ message }}</h1>
    <a>This app uses the Coin Market Cap's public API</a> <a href="https://coinmarketcap.com/api/">(https://coinmarketcap.com/api).</a>
    <a>Please, be consider and do not make more than 10 requests per minute.</a>
  </div>
</template>

<script>
export default {
  data () {
    return {
      message: 'Welcome to CryptoCoinMarket'
    }
  }
}
</script>

<style>
.container {
  margin-top: 60px;
}

</style>
