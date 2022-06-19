<template>
  <button @click="onClick" :class="{ active: active, not_active: !active }">
    {{ placeholder }}
  </button>
</template>

<script>
export default {
  props: ["placeholder", "active"],
  methods:{
    onClick(e){
      if(this.active){
        this.$emit('onClick', e)
      }
    }
  }
};
</script>

<style lang="scss" scoped>
button {
  width: 100%;
  padding: 10px 0;
  border-radius: 10px;
  border: none;
  outline: none;
  cursor: pointer;
  font-family: Inter;
  font-size: 12px;
  font-weight: 600;
  text-align: center;
}

.active {
  background: $background-green;
  color: $font-white;
}

.not_active {
  background: $background-grey;
  color: $font-grey;
}
</style>