<script setup>
import { ref } from "vue";
import { isNum } from "../helpers/helpers";

const isInvalid = ref(false)

function validate(value) {
  isInvalid.value = (value.match(/\./g) || []).length > 1 || value < 0 ? true : false
  return !isInvalid.value && value != '' && value >= 0 ? parseFloat(value) : 0
}
</script>

<template>
  <div class="bill">
    <label for="bill-amount">Bill</label>
    <input
      @keypress="isNum($event)"
      @change="$emit('setBill', validate($event.target.value))"
      type="text"
      name="bill-amount"
      id="bill-amount"
      minlength="1"
      maxlength="6"
      :class="{ invalid: isInvalid }"
      placeholder="0"
    />
  </div>
</template>

<style lang="scss">
.bill {
  display: flex;
  flex-direction: column;
  gap: 10px;

  label {
    text-align: left;
  }

  input {
    background-color: variables.$very-light-grayish-cyan;
    background-image: url('../assets/images/icon-dollar.svg');
    background-repeat: no-repeat;
    background-position: 15px;

    border: none;
    height: 45px;
    width: 100%;
    text-align: right;
    font-size: 24px;
    padding: 0 15px;

    border-radius: 5px;

    cursor: pointer;
  }
}
</style>
