<template>
  <div class="container_card" @mouseover="hover = true" @mouseout="hover = false">
    <transition name="transition_delete">
      <button class="delete" v-if="hover" @click="onDelete">
        <svg
          width="14"
          height="16"
          viewBox="0 0 14 16"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M1.56294 4.76335V13.9953C1.56294 14.541 1.76303 15.0534 2.11256 15.4211C2.46048 15.7898 2.94467 15.9991 3.4514 16H10.541C11.0478 15.9991 11.532 15.7898 11.8798 15.4211C12.2293 15.0534 12.4294 14.541 12.4294 13.9953V4.76335C13.1242 4.57893 13.5745 3.90768 13.4815 3.19471C13.3884 2.48189 12.7811 1.94867 12.0622 1.94852H10.1437V1.48014C10.1459 1.08626 9.99017 0.708039 9.71134 0.42979C9.4325 0.151688 9.0537 -0.0031709 8.65982 4.92333e-05H5.33255C4.93867 -0.0031709 4.55986 0.151688 4.28103 0.42979C4.00219 0.708039 3.84646 1.08626 3.84865 1.48014V1.94852H1.93019C1.21122 1.94867 0.603931 2.48189 0.51084 3.19471C0.417896 3.90768 0.868128 4.57893 1.56294 4.76335ZM10.541 15.2506H3.4514C2.81075 15.2506 2.31236 14.7002 2.31236 13.9953V4.79629H11.68V13.9953C11.68 14.7002 11.1816 15.2506 10.541 15.2506ZM4.59806 1.48014C4.59558 1.28503 4.67227 1.09724 4.81074 0.959502C4.94906 0.821768 5.13729 0.746095 5.33255 0.749461H8.65982C8.85508 0.746095 9.04331 0.821768 9.18163 0.959502C9.32009 1.09709 9.39679 1.28503 9.3943 1.48014V1.94852H4.59806V1.48014ZM1.93019 2.69793H12.0622C12.4347 2.69793 12.7367 2.99989 12.7367 3.3724C12.7367 3.74491 12.4347 4.04688 12.0622 4.04688H1.93019C1.55768 4.04688 1.25571 3.74491 1.25571 3.3724C1.25571 2.99989 1.55768 2.69793 1.93019 2.69793Z"
            fill="white"
          />
        </svg>
      </button>
    </transition>
    <img :src="image" :alt="name" />
    <h3>{{ name }}</h3>
    <p>{{ description }}</p>
    <h3>{{ getPrice }} руб.</h3>
  </div>
</template>

<script>
export default {
  name: "NuxtTutorial",
  props: ["price", "name", "description", "image"],
  data() {
    return { hover: false };
  },
  computed:{
    getPrice(){
      return String(this.price).replace(/(\d)(?=(\d{3})+([^\d]|$))/g, '$1 ');
    }
  },
  methods:{
    onDelete(){
      if(this.hover){
        this.$emit('onDelete', this.name)
      }
    }
  }
};
</script>

<style lang="scss" scoped>
.container_card {
  width: 100%;
  height: 423px;
  border-radius: 4px;
  position: relative;
  background: $background-white;

  transition: all 1s;
  cursor: pointer;

  .delete {
    border: none;
    outline: none;
    position: absolute;
    display: flex;
    align-items: center;
    justify-content: center;
    top: -10px;
    right: -10px;
    width: 32px;
    height: 32px;
    background: $backround-red;
    box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
    border-radius: 10px;
  }

  .transition_delete-enter-active,
  .transition_delete-leave-active {
    transition: opacity 0.5s;
  }
  .transition_delete-enter, .transition_delete-leave-to {
    opacity: 0;
  }

  img {
    width: 100%;
    height: 200px;
    border-radius: 4px 4px 0px 0px;
  }
  p {
    margin: 0 16px 0 16px;
  }
  h3 {
    margin: 25px 16px 20px 16px;
  }
}
</style>
