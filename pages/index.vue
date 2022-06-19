<template>
  <div class="home_container">
    <AddNewProduct @addProduct="AddProduct" />
    <div class="selector_and_list">
      <SelectComponent
        :array="select"
        :value="select_value"
        @onInput="select_value = $event"
      />
      <transition-group name="grid_products" class="grid_products">
        <ProductCard
          v-for="product in products_array"
          :key="product.id"
          :name="product.name"
          :price="product.price"
          :description="product.description"
          :image="product.image"
          @onDelete="DeleteProduct(product.id)"
        />
      </transition-group>
    </div>
  </div>
</template>

<script>
export default {
  mounted() { //здесь должен быть запрос на сервер
    let products_storage = JSON.parse(localStorage.getItem("products"));

    if (Array.isArray(products_storage)) {
      this.products = products_storage;
    } else {
      this.products = this.products_default //костыль, за что извиняюсь
    }
  },
  methods: {
    SetStoreProducts() {
      localStorage.setItem("products", JSON.stringify(this.products));
    },
    DeleteProduct(id) {
      this.products = this.products.filter((element) => element.id !== id);
      this.SetStoreProducts();
    },
    AddProduct(element) {
      this.products = [
        ...this.products,
        {
          id: this.products.reverse()[0]
            ? this.products.reverse()[0].id + 1
            : 0,
          name: element.name,
          description: element.description,
          image: element.image,
          price: element.price,
        },
      ];
      this.SetStoreProducts();
    },
  },
  computed: {
    products_array() {
      let result = [...this.products];
      switch (this.select_value) {
        case "По наименованию":
          result.sort((a, b) =>
            a.name.toLowerCase() > b.name.toLowerCase() ? 1 : -1
          );
          break;
        case "По цене min":
          result.sort((a, b) => a.price - b.price);
          break;
        case "По цене max":
          result.sort((a, b) => b.price - a.price);
          break;
      }
      return result;
    },
  },
  data() {
    return {
      select_value: "По умолчанию",
      select: ["По умолчанию", "По наименованию", "По цене min", "По цене max"],
      products:[],
      products_default: [
        {
          id: 0,
          name: "Наименование товара",
          price: "1000",
          description:
            "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          image: "https://i.imgur.com/JSvsRG2.png",
        },
        {
          id: 1,
          name: "аименование товара",
          price: "10000",
          description:
            "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          image: "https://i.imgur.com/JSvsRG2.png",
        },
        {
          id: 2,
          name: "ваименование товара",
          price: "10000",
          description:
            "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          image: "https://i.imgur.com/JSvsRG2.png",
        },
        {
          id: 3,
          name: "Наименование товара",
          price: "10000",
          description:
            "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          image: "https://i.imgur.com/JSvsRG2.png",
        },
        {
          id: 4,
          name: "Наименование товара",
          price: "10000",
          description:
            "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          image: "https://i.imgur.com/JSvsRG2.png",
        },
        {
          id: 5,
          name: "Наименование товара",
          price: "10000",
          description:
            "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          image: "https://i.imgur.com/JSvsRG2.png",
        },
        {
          id: 6,
          name: "Наименование товара",
          price: "10000",
          description:
            "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          image: "https://i.imgur.com/JSvsRG2.png",
        },
        {
          id: 7,
          name: "Наименование товара",
          price: "10000",
          description:
            "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          image: "https://i.imgur.com/JSvsRG2.png",
        },
        {
          id: 9,
          name: "Наименование товара",
          price: "10000",
          description:
            "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          image: "https://i.imgur.com/JSvsRG2.png",
        },
        {
          id: 10,
          name: "Наименование товара",
          price: "10000",
          description:
            "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          image: "https://i.imgur.com/JSvsRG2.png",
        },
      ],
    };
  },
};
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "SourceSansPro";
}

.home_container {
  display: flex;
  justify-content: space-around;
  max-height: 100vh;
  min-height: 100vh;
  width: 100%;
  background: $main-backround;
  @media (max-width: 750px) {
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;
    max-height: 100%;
  }
  .selector_and_list {
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    overflow: auto;
    select {
      margin: 32px 32px 0 16px;
      @media (max-width: 750px) {
        margin: 32px 16px 0 16px;
        width: 332px;
      }
    }
    &::-webkit-scrollbar {
      display: none;
      width: 0;
      height: 0;
    }
    .grid_products {
      padding: 16px 32px 32px 16px;
      /*display: flex;
      justify-content: flex-start;
      flex-wrap: wrap;*/
      display: grid;
      grid-template-columns: repeat(4, 332px);
      grid-column-gap: 16px;
      grid-row-gap: 16px;
      @media (max-width: 1800px) {
        grid-template-columns: repeat(3, 332px);
      }
      @media (max-width: 1450px) {
        grid-template-columns: repeat(2, 332px);
      }
      @media (max-width: 1100px) {
        grid-template-columns: repeat(1, 332px);
      }
      @media (max-width: 750px) {
        padding: 16px 16px 16px 16px;
      }
    }
    .grid_products-enter,
    .grid_products-leave-to {
      opacity: 0;
    }
  }
}
</style>
