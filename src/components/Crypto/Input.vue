<script>
export default {
  props: {
    changeAmount: {
      type: Function,
      required: true,
    },
  },
  data() {
    return {};
  },
};
</script>

<template>
  <input
    @input="changeAmount($event.target.value)"
    type="number"
    min="0"
    placeholder="coin"
  />
</template>

<style lang="scss" scoped>
input {
  margin-top: 10px;
  width: 100%;
  padding: 10px;
  &::-webkit-inner-spin-button,
  &::-webkit-outer-spin-button {
    -webkit-appearance: none;
    margin: 0;
  }
  &::-moz-appearance {
    appearance: none;
  }
  appearance: textfield;
}
</style>
