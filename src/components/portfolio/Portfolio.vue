<template>
  <div class="card-deck">
    <app-stock v-for="stock in stocks" :key="stock.name" :stock="stock"></app-stock>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import Stock from './Stock.vue'

export default {
  computed: {
    ...mapGetters({
      stocks: 'stockPortfolio'
    })
  },
  components: {
    appStock: Stock
  }
}
</script>
