<script>
export default {
  props: {
    fav: {
      type: Array,
      require: true,
    },
    getFromFav: {
      type: Function,
      require: true,
    },
  },
};
</script>

<template>
  <div className="favorite">
    <ul @click="getFromFav(index)" v-for="(item, index) in fav" :key="index">
      <li>{{ item.to }}</li>
      <li>{{ item.from }}</li>
    </ul>
  </div>
</template>

<style lang="scss" scoped>
.favorite {
  ul {
    display: flex;
    justify-content: space-between;
    margin-left: 20px;
    margin-right: 20px;
    cursor: pointer;
    &:hover {
      transform: scale(1.1);
      transition: all 1s ease;
    }
    li {
      display: flex;
      margin-top: 10px;
      background-color: rgb(255, 0, 179);
      list-style: none;
      padding: 10px;
      color: aliceblue;
    }
  }
}
</style>
