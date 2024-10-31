<script>
export default {
  props: {
    setCrypto: {
      type: Function,
      required: true,
    },
    cryptoNow: {
      type: String,
      required: true,
    }
  },
};
</script>

<template>
  <ul>
    <li
      @click="setCrypto('BTC')"
      :class="{ active: cryptoNow === 'BTC' }"
    >
      BTC
    </li>
    <li
      @click="setCrypto('ETH')"
      :class="{ active: cryptoNow === 'ETH' }"
    >
      ETH
    </li>
    <li
      @click="setCrypto('USDT')"
      :class="{ active: cryptoNow === 'USDT' }"
    >
      USDT
    </li>
  </ul>
</template>

<style scoped>
ul {
  width: 120px;
  height: 120px;
  background-color: darkslateblue;
  display: flex;
  flex-direction: column;
  justify-content: space-around;


  border: 2px solid #4b0082;
}
li {
  list-style: none;
  color: bisque;
}
li:hover,
li.active {
  cursor: pointer;
  background: darkblue;
}
</style>
