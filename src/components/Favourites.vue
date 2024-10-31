<script>
export default {
  data() {
    return {};
  },
  props: {
    favs: {
      type: Array,
      requires: true,
    },
    getFromFavs: {
      type: Function,
      required: true,
    },
  },
};
</script>

<template>
  <h2>Options in favourites</h2>
  <div @click="getFromFavs(index)" class="favourites" v-for="(el, index) of favs" :key="index">
    <span>{{ el.from }}</span>
    <span>{{ el.to }}</span>
  </div>
</template>

<style>
.favourites {
  display: flex;
  justify-content: space-between;
  width: 400px;
  margin: 0 auto;
  transition: all 500ms ease;
  margin-bottom: 10px;
}

span {
  padding: 10px 15px;
  background: #8c00ff;
  color: white;
}
.favourites:hover {
  opacity: 0.7;
  transform: scale(1.1);
  cursor: pointer;
}
</style>
