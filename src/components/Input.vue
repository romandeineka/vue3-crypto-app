<script>
export default {
  props: {
    changeAmount: {
      type: Function,
      required: true,
    },
    convertCrypto: {
      type: Function,
      required: true
    },
    favourite: {
      type: Function,
      required: true
    }
  },
};
</script>

<template>
  <div class="wrap">
    <input
      min="0"
      class="input"
      @input="changeAmount($event.target.value)"
      type="number"
      placeholder="Enter a number"
    />
    <div class="wrap-btn">
      <button @click="convertCrypto()">To convert</button>
      <button @click="favourite()">Favourites</button>
    </div>
  </div>
</template>

<style scoped>
.input {
  outline: none;
  border: none;
  width: 400px;
  height: 30px;
  margin-block: 50px 30px;
  padding: 5px;
}
.wrap {
  display: flex;
  flex-direction: column;
  align-items: center;
}

button {
  text-transform: uppercase;
  background: darkslateblue;
  border: none;
  color: white;
  height: 30px;
  width: 100px;
  border-radius: 5px;
  cursor: pointer;
}

.wrap-btn {
  display: flex;
  gap: 30px;
}
</style>
