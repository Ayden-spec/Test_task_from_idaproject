<template>
  <select
    name="roleSelector"
    id="role_selector"
    @change="$emit('onInput', $event.target.value)"
    :value="value"
  >
    <option v-for="(element, index) in array" :key="index" :value="element">
      {{ element }}
    </option>
  </select>
</template>

<script>
export default {
  props: ["value", "array"],
};
</script>

<style lang="scss" scoped>
select {
  border: none;
  outline: none;
  padding: 10px;
  color: $font-grey;

  appearance: none;

  width: 150px;
  height: 36px;

  background-blend-mode: multiply;

  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  background-size: 5px 5px;
  background: url("data:image/svg+xml,%3Csvg width='8' height='6' viewBox='0 0 8 6' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M7.48532 1.24264L4.24268 4.48528L1.00003 1.24264' stroke='%23B4B4B4'/%3E%3C/svg%3E")
    no-repeat right $background-white_two;
  background-position-x: calc(100% - 10px);
}
</style>