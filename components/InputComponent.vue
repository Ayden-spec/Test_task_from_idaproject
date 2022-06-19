<template>
  <label>
    <span class="placeholder">
      <span>{{ placeholder }}</span>
      <div class="placeholder_dot" v-if="required" />
    </span>
    <input
      :class="{ border_focus: focus_active }"
      :type="type"
      :placeholder="placeholderIput"
      @input="onInput"
      :value="value"
      @focus="hasFocus"
    />
    <p v-if="focus_active">Поле является обязательным</p>
  </label>
</template>

<script>
export default {
  props: ["placeholder", "placeholderIput", "type", "value", "required"],
  data() {
    return {
      focus_active: false,
    };
  },
  methods: {
    hasFocus() {
      if (this.required) {
        this.focus_active = true;
      }
    },
    onInput(event) {
      let text = event.target.value.trim();
      if (text.length === 0 && this.required) {
        this.focus_active = true;
      } else {
        this.focus_active = false;
      }
      this.$emit("onInput", text);
    },
  },
};
</script>

<style lang="scss" scoped>
label {
  display: inline-block;
  width: 100%;
  .placeholder {
    position: relative;
    font-size: 10px;
    font-weight: 400;
    .placeholder_dot {
      position: absolute;
      width: 4px;
      height: 4px;
      top: 0;
      right: -4px;
      background: $backround-red;
      border-radius: 50%;
    }
  }
  p {
    color: $backround-red;
    font-size: 8px;
    font-weight: 400;
  }
  .border_focus {
    border: 1px solid $backround-red;
  }
  input {
    border: none;
    outline: none;
    background: transparent;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    padding: 7px 9px;
    width: 100%;
    margin-top: 5px;
    font-size: 12px;
    font-weight: 400;
    &::placeholder {
      color: $font-grey;
    }
  }
}
</style>
