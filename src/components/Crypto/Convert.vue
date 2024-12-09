<script>
import CryptoConvert from "crypto-convert";
import Selector from "./Selector.vue";
import Input from "./Input.vue";
import Favorite from "./Favorite.vue";

const convert = new CryptoConvert();

export default {
  components: {
    Selector,
    Input,
    Favorite,
  },
  data() {
    return {
      amount: 0,
      cryptoFirst: "",
      cryptoSecond: "",
      error: "",
      result: 0,
      fav: [],
    };
  },
  methods: {
    favorite() {
      const cryptoFav = {
        to: this.cryptoFirst,
        from: this.cryptoSecond,
      };
      this.fav.push(cryptoFav);
      console.log(cryptoFav);
    },
    getFromFav(index) {
      this.cryptoFirst = this.fav[index].to;
      this.cryptoSecond = this.fav[index].from;
    },
    changeAmount(value) {
      this.amount = value;
    },
    setFirstSelector(value) {
      this.cryptoFirst = value;
      console.log(this.cryptoFirst);
    },
    setSecondSelector(value) {
      this.cryptoSecond = value;
      console.log(this.cryptoSecond);
    },
    async convert() {
      if (this.amount > 0) {
        this.error = "";
      }
      if (this.amount <= 0) {
        this.error = "Выбирите другую сумму!";
        this.result = 0;
        return;
      } else if (this.cryptoFirst === this.cryptoSecond) {
        this.error = "Выбирите другую валюту!";
        return;
      } else if (this.cryptoFirst == "" || this.cryptoSecond == "") {
        this.error = "Выбирите другую валюту!";
        return;
      }

      await convert.ready();
      if (this.cryptoFirst == "BTC" && this.cryptoSecond == "ETH") {
        this.result = convert.BTC.ETH(this.amount) + " " + this.cryptoSecond;
      } else if (this.cryptoFirst == "BTC" && this.cryptoSecond == "USDT") {
        this.result = convert.BTC.USDT(this.amount) + " " + this.cryptoSecond;
      } else if (this.cryptoFirst == "ETH" && this.cryptoSecond == "BTC") {
        this.result = convert.ETH.BTC(this.amount) + " " + this.cryptoSecond;
      } else if (this.cryptoFirst == "ETH" && this.cryptoSecond == "USDT") {
        this.result = convert.ETH.USDT(this.amount) + " " + this.cryptoSecond;
      } else if (this.cryptoFirst == "USDT" && this.cryptoSecond == "BTC") {
        this.result = convert.USDT.BTC(this.amount) + " " + this.cryptoSecond;
      } else if (this.cryptoFirst == "USDT" && this.cryptoSecond == "ETH") {
        this.result = convert.USDT.ETH(this.amount) + " " + this.cryptoSecond;
      }
    },
  },
};
</script>

<template>
  <div className="crypto__convert">
    <h1>Crypto</h1>
    <Input :changeAmount="changeAmount" />
    <button @click="convert()">Конвертировать</button>
    <button @click="favorite()">Favorite</button>
    <p v-if="result !== ''" className="crypto__result">{{ result }}</p>
    <Favorite v-if="fav.length > 0" :fav="fav" :getFromFav="getFromFav" />
    <p v-if="error !== ''">{{ error }}</p>
    <dir className="selectors">
      <Selector :setCrypto="setFirstSelector" :cryptoNow="cryptoFirst" />
      <Selector :setCrypto="setSecondSelector" :cryptoNow="cryptoSecond" />
    </dir>
  </div>
</template>

<style lang="scss" scoped>
@import url("https://fonts.googleapis.com/css2?family=Nabla:EDPT@120&family=Space+Mono:ital,wght@0,400;0,700;1,400;1,700&display=swap");
h1 {
  width: 100%;
  display: flex;
  justify-content: center;
  text-align: center;
  font-size: 120px;
  font-family: "Nabla", cursive;
}
.crypto__result {
  display: flex;
  justify-content: center;
  margin-top: 15px;
  margin-bottom: 15px;
  font-family: "Nabla", cursive;
  font-size: 20px;
}

.crypto__convert {
  width: 100%;
  position: relative;
  left: 50%;
  right: 50%;
  top: 100px;
  max-width: 500px;
  height: auto;

  button {
    display: block;
    margin: 50px auto 0 auto;
    padding: 20px 50px;
    background-color: black;
    color: red;
    font-size: 20px;
    border: none;
    cursor: pointer;
    user-select: none;
  }
  .selectors {
    display: flex;
    justify-content: space-between;
  }
}
</style>
