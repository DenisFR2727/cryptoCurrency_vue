<script>
export default {
  props: {
    setCrypto: {
      type: Function,
      require: true,
    },
    cryptoNow: {
      type: String,
      require: true,
    },
  },
};
</script>

<template>
  <ul>
    <li
      @click="setCrypto('BTC')"
      :className="cryptoNow == 'BTC' ? 'active' : ''"
    >
      BTC
    </li>
    <li
      @click="setCrypto('ETH')"
      :className="cryptoNow == 'ETH' ? 'active' : ''"
    >
      ETH
    </li>
    <li
      @click="setCrypto('USDT')"
      :className="cryptoNow == 'USDT' ? 'active' : ''"
    >
      USDT
    </li>
  </ul>
</template>

<style lang="scss" scoped>
ul {
  margin-top: 20px;
  li {
    padding: 10px 70px;
    list-style: none;
    background-color: rgb(107, 98, 98);
    cursor: pointer;
    user-select: none;
  }
  .active {
    background-color: rgba(137, 78, 78, 0.814);
  }
}
</style>
