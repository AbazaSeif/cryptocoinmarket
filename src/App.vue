<template>
  <div id="app">
    <welcome></welcome>
    <global-info></global-info>
    <crypto-finder></crypto-finder>
  </div>
</template>

<script>
import Welcome from './components/Welcome'
import GlobalInfo from './components/GlobalInfo'
import CryptoFinder from './components/CryptoFinder'

export default {
  name: 'app',
  components: {
    'welcome': Welcome,
    'global-info': GlobalInfo,
    'crypto-finder': CryptoFinder
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
