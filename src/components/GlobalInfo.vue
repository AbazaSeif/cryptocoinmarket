<template>
  <div class="container">
    <h2>{{ message }}</h2>
    <table border="5" cellpadding="8" cellspacing="4">
      <tr>
        <th>Active assets</th>
        <th>Active currencies</th>
        <th>Active markets</th>
        <th>Bitcoin percentage of market capital</th>
        <th>Total 24h volume (usd)</th>
        <th>Total market capital (usd)</th>
      </tr>
      <tr>
        <td>{{ active_assets }} assets</td>
        <td>{{ active_currencies }} curencies</td>
        <td>{{ active_markets }} markets</td>
        <td>{{ bitcoin_percentage_of_market_cap }} %</td>
        <td>{{ total_24h_volume_usd }} $</td>
        <td>{{ total_market_cap_usd }} $</td>
      </tr>
    </table>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data () {
    return {
      message: 'Global Data Market',
      active_assets: 0,
      active_currencies: 0,
      active_markets: 0,
      bitcoin_percentage_of_market_cap: 0,
      total_24h_volume_usd: 0,
      total_market_cap_usd: 0
    }
  },
  created: function () {
    this.loadInfo()
  },
  methods: {
    loadInfo: function () {
      axios.get('https://api.coinmarketcap.com/v1/global/')
      .then((response) => {
        this.active_assets = response.data.active_assets
        this.active_currencies = response.data.active_currencies
        this.active_markets = response.data.active_markets
        this.bitcoin_percentage_of_market_cap = response.data.bitcoin_percentage_of_market_cap
        this.total_24h_volume_usd = response.data.total_24h_volume_usd
        this.total_market_cap_usd = response.data.total_market_cap_usd
      })
    }
  }
}
</script>

<style>
  .container {
    width:100%;
    height:100%;
    margin-top: 40px;
  }

  table {
    margin: 0 auto;
  }
</style>
