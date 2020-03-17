<template>
  <div>
    <h1>
      Current Bitcoin Rate:
      <br />
      1 BTC = {{this.bitcoinRate}} €
    </h1>

    <h3>
      Bought for:
      <br />
      1 BTC = {{this.boughtRate}} €
    </h3>

    <h1 v-bind:class="{ success: this.isProfit, failure: !this.isProfit }">
      Profit?
      <br />
      {{this.isProfit?"YES":"NO :("}}
      <br />
      {{this.profit}} €
    </h1>

    <h3>
      Current value:
      <br />
      {{this.boughtAmount}} BTC * {{this.bitcoinRate}} €
      <br />
      {{this.boughtAmount * this.bitcoinRate}} €
    </h3>

    <div class="box">
      <div class="input-container">
        <input v-model="customCalculation" type="text" required />
        <label>Custom calculation</label>
      </div>
      <p>{{ customCalculation * bitcoinRate }} €</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      bitcoinRate: 4927.37,
      boughtAmount: 1.0,
      boughtRate: 4999.48,
      isProfit: true,
      profit: 0,
      customCalculation: null
    };
  },
  beforeMount() {
    this.getProfit();
  },
  methods: {
    async getCurrentRate() {
      let result = await this.axios.get("https://blockchain.info/ticker");
      let rate = result.data.EUR.last;
      this.bitcoinRate = Number(rate).toFixed(2);
    },
    async getProfit() {
      await this.getCurrentRate();
      if (this.bitcoinRate > this.boughtRate) this.isProfit = true;
      else this.isProfit = false;
      this.profit =
        this.boughtAmount * this.bitcoinRate -
        this.boughtAmount * this.boughtRate;
      this.profit = this.profit.toFixed(2);
    }
  }
};
</script>

<style scoped>
.failure {
  color: tomato;
}
.success {
  color: aquamarine;
}
@import url("https://fonts.googleapis.com/css?family=Noto+Sans:400,400i,700,700i&subset=greek-ext");

.box {
  margin: 30px 0px 0px 0px;
  padding: 10px 100px;
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
.input-container {
  position: relative;
  margin-bottom: 5px;
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
.input-container label {
  position: absolute;
  top: 0px;
  left: 0px;
  font-size: 16px;
  color: #8c8100;
  pointer-event: none;
  transition: all 0.5s ease-in-out;
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
.input-container input {
  border: 0;
  border-bottom: 1px solid #555;
  background: transparent;
  width: 100%;
  padding: 8px 0 5px 0;
  font-size: 16px;
  color: #8c8100;
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
.input-container input:focus {
  border: none;
  outline: none;
  border-bottom: 1px solid #7847ff;
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
.input-container input:focus ~ label,
.input-container input:valid ~ label {
  top: -12px;
  font-size: 12px;
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
</style>
