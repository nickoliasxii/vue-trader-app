<template>
  <div class="card">
    <div class="card-header">
      <h4 class="card-title">
        {{ stock.name }}
      </h4>
    </div>
    <div class="card-body row">
      <div class="w-75">
        <input
          type="number"
          class="form-control"
          placeholder="Quantity"
          v-model.number="quantity"
          :class="{danger: insufficientFunds}"
        >
      </div>
      <div class="w-25">
        <button
          class="btn btn-success"
          @click="buyStock"
          :disabled=" insufficientFunds || quantity <= 0 || !Number.isInteger(quantity)"
        >{{ insufficientFunds ? 'Insufficient Funds' : 'Buy'}}</button>
      </div>
    </div>
    <div class="card-footer">
      <small class="small-text">(Price: {{ stock.price }})</small>
    </div>
  </div>
</template>

<script>
export default {
  props: ['stock'],
  data() {
    return {
      quantity: 0
    }
  },
  computed: {
    funds() {
      return this.$store.getters.funds
    },
    insufficientFunds() {
      return this.quantity * this.stock.price > this.funds
    }
  },
  methods: {
    buyStock() {
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        quantity: this.quantity
      }
      this.$store.dispatch('buyStock', order)
      this.quantity = 0
    }
  }
}
</script>

<style scoped>
.danger {
  border: 1px solid red;
}
</style>

