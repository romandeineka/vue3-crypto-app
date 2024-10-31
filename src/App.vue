<script>
import Input from "./components/Input.vue";
import Selector from "./components/Selector.vue";
import Favourites from "./components/Favourites.vue";
import CryptoConvert from "crypto-convert";

const convert = new CryptoConvert(/*options?*/);

export default {
  components: {
    Input,
    Selector,
    Favourites,
  },
  data() {
    return {
      amount: 0,
      cryptoFirst: "",
      cryptoSecond: "",
      error: "",
      result: 0,
      favs: [],
    };
  },
  methods: {
    changeAmount(value) {
      this.amount = value;
    },
    setCryptoFirst(value) {
      this.cryptoFirst = value;
    },
    setCryptoSecond(value) {
      this.cryptoSecond = value;
    },
    async convertCrypto() {
      if (this.cryptoFirst === "" || this.cryptoSecond === "") {
        this.error = "Select a cryptocurrency!";
        return;
      }
      if (this.cryptoFirst === this.cryptoSecond) {
        this.error = "Select different cryptocurrency pairs!";
        return;
      }
      if (this.amount <= 0) {
        this.error = "Enter a value greater than 0!";
        return;
      }

      this.error = "";
      await convert.ready();

      if (this.cryptoFirst === "BTC" && this.cryptoSecond === "ETH") {
        this.result = convert.BTC.ETH(this.amount);
      }
      if (this.cryptoFirst === "BTC" && this.cryptoSecond === "USDT") {
        this.result = convert.BTC.USDT(this.amount);
      }
      if (this.cryptoFirst === "ETH" && this.cryptoSecond === "BTC") {
        this.result = convert.ETH.BTC(this.amount);
      }
      if (this.cryptoFirst === "ETH" && this.cryptoSecond === "USDT") {
        this.result = convert.ETH.USDT(this.amount);
      }
      if (this.cryptoFirst === "USDT" && this.cryptoSecond === "BTC") {
        this.result = convert.USDT.BTC(this.amount);
      }
      if (this.cryptoFirst === "USDT" && this.cryptoSecond === "ETH") {
        this.result = convert.USDT.ETH(this.amount);
      }
    },
    favourite() {
      this.favs.push({
        from: this.cryptoFirst,
        to: this.cryptoSecond,
      });
    },
    getFromFavs(index) {
      this.cryptoFirst = this.favs[index].from;
      this.cryptoSecond = this.favs[index].to;
    },
  },
};
</script>

<template>
  <h1>crypto</h1>
  <Input
    :favourite="favourite"
    :changeAmount="changeAmount"
    :convertCrypto="convertCrypto"
  />
  <p class="error">{{ error }}</p>
  <p v-if="result !== 0" class="result">{{ result }}</p>
  <Favourites :getFromFavs="getFromFavs" :favs="favs" v-if="favs.length > 0" />
  <div class="selectors">
    <Selector :cryptoNow="cryptoFirst" :setCrypto="setCryptoFirst" />
    <Selector :cryptoNow="cryptoSecond" :setCrypto="setCryptoSecond" />
  </div>
</template>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Bebas+Neue&display=swap");
.selectors {
  width: 600px;
  display: flex;
  justify-content: space-around;
  margin: 0 auto;
}
.error {
  color: gold;
  margin-bottom: 10px;
}
.result {
  font-family: "Bebas Neue", sans-serif;
  font-size: 36px;
  color: gold;
}
</style>
