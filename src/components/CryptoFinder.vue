<template>
  <div class="container">
    <h2>Select a badge to show related information*</h2>
    <h4>* Price and Market capital</h4>
    <select id="select" ref="selector" @change="onSelectorChanged ()"></select>
    <button @click="onSubmitClicked ()">Submit</button>
    <table border="5" cellpadding="8" cellspacing="4">
      <tr>
        <th>Coin name</th>
        <th>Price($)</th>
        <th>Price(BTC)</th>
        <th>24h volume(us)</th>
        <th>Market cap(us)</th>
        <th>Available supply</th>
        <th>Percent change 1h</th>
        <th>Percent change 24h</th>
        <th>Percent change 7d</th>
        <th>Last updated</th>
        <th>Price ({{ this.current_badge }})</th>
        <th>Market cap({{ this.current_badge }})</th>
      </tr>
      <tr v-for="currency in currencies">
        <td>{{ currency.name }}</td>
        <td>{{ currency.price_usd }}</td>
        <td>{{ currency.price_btc }}</td>
        <td></td>
        <td>{{ currency.market_cap_usd }}</td>
        <td>{{ currency.available_supply }}</td>
        <td>{{ currency.percent_change_1h }}</td>
        <td>{{ currency.percent_change_24h }}</td>
        <td>{{ currency.percent_change_7d }}</td>
        <td>{{ printableDate (currency.last_updated) }}</td>
        <td>{{ getBadgeSelectedPrice (currency) }}</td>
        <td>{{ getBadgeSelectedMarketCap (currency) }}</td>
      </tr>

    </table>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data () {
    return {
      current_badge: 'eur',
      currencies: [],
      badges: ['AUD', 'BRL', 'CAD', 'CHF', 'CLP', 'CNY', 'CZK', 'DKK', 'EUR', 'GBP', 'HKD', 'HUF', 'IDR', 'ILS', 'INR', 'JPY', 'KRW', 'MXN', 'MYR', 'NOK', 'NZD', 'PHP', 'PKR', 'PLN', 'RUB', 'SEK', 'SGD', 'THB', 'TRY', 'TWD', 'US', 'ZAR']
    }
  },
  mounted: function () {
    this.getCurrencies()
    this.loadSelectorEntries()
  },
  methods: {
    getBadgeSelectedPrice: function (currency) {
      var aux = 'price_' + this.current_badge
      return currency[aux]
    },
    getBadgeSelectedMarketCap: function (currency) {
      var aux = 'market_cap_' + this.current_badge
      return currency[aux]
    },
    loadSelectorEntries: function () {
      var selector = this.$refs.selector
      for (var i = 0; i <= this.badges.length; i++) {
        var option = null
        option = document.createElement('option')
        option.value = this.badges[i]
        option.innerHTML = this.badges[i]
        if (this.badges[i] === 'EUR') {
          option.selected = 'selected'
        }
        selector.appendChild(option)
      }
    },
    getCurrencies: function () {
      axios.get('https://api.coinmarketcap.com/v1/ticker/', {
        params: {
          convert: this.current_badge
        }
      })
      .then((response) => {
        this.currencies = response.data
      })
    },
    printableDate: function (timestamp) {
      var date = new Date(timestamp * 1000)
      // Hours part from the timestamp
      var hours = date.getHours()
      // Minutes part from the timestamp
      var minutes = '0' + date.getMinutes()
      // Seconds part from the timestamp
      var seconds = '0' + date.getSeconds()

      // Will display time in 10:30:23 format
      var formattedTime = hours + ':' + minutes.substr(-2) + ':' + seconds.substr(-2)
      return formattedTime
    },
    onSelectorChanged: function () {
      var selector = this.$refs.selector
      this.current_badge = selector.value.toLowerCase()
      console.log('New badge selected: ' + this.current_badge)
    },
    onSubmitClicked: function () {
      this.getCurrencies()
    }
  }
}
</script>

<style>
.container {
  margin-top: 40px;
}

button {
    margin-bottom: 40px;
}
</style>
