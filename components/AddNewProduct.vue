<template>
  <div class="add_new_product_container">
    <h2>Добавление товара</h2>
    <div class="card_add_new_product">
      <InputComponent
        placeholder="Наименование товара"
        placeholderIput="Введите наименование товара"
        :required="true"
        type="text"
        :value="input_name"
        @onInput="input_name = $event"
      />
      <TextareaComponent
        placeholder="Описание товара"
        placeholderIput="Введите описание товара"
        :required="false"
        :value="input_description"
        @onInput="input_description = $event"
      />
      <InputComponent
        placeholder="Ссылка на изображение товара"
        placeholderIput="Введите ссылку"
        :required="true"
        type="text"
        :value="input_image"
        @onInput="input_image = $event"
      />
      <InputComponent
        placeholder="Цена товара"
        placeholderIput="Введите цену"
        :required="true"
        type="number"
        :value="input_price"
        @onInput="input_price = $event"
      />
      <ButtonComponent
        placeholder="Добавить товар"
        :active="active_button"
        @onClick="addNewProduct"
      />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      input_name: "",
      input_description: "",
      input_image: "",
      input_price: "",
    };
  },
  computed: {
    active_button() {
      return (
        !!this.input_name.length &&
        !!this.input_image.length &&
        !!this.input_price.length
      );
    },
  },
  methods: {
    addNewProduct() {
      if (this.active_button && this.input_price > 0) {
        this.$emit("addProduct", {
          name: this.input_name,
          description: this.input_description,
          image: this.input_image,
          price: this.input_price,
        });
        this.input_name = "";
        this.input_description = "";
        this.input_image = "";
        this.input_price = "";
      }
    },
  },
};
</script>

<style lang='scss' scoped>
.add_new_product_container {
  margin: 32px 0 0 32px;
  @media (max-width: 750px) {
    margin: 32px 16px 0 16px;
  }
  h2 {
    margin: 0 0 16px 0;
    height: 36px;
  }
  .card_add_new_product {
    width: 332px;
    height: 440px;
    padding: 24px;

    background: $background-white_two;
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
      0px 6px 10px rgba(0, 0, 0, 0.02);
    border-radius: 4px;

    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }
}
</style>
