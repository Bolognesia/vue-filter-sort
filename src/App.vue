<template>
  <div
    class="sort-btn-wrapper"
    @click="sort_reverse = !sort_reverse"
    :class="{ filterOn: sort_alph }"
    >
    <div class="sort-btn" v-if="!sort_reverse">A-Z</div>
    <div class="sort-btn" v-if="sort_reverse">Z-A</div>
  </div>

  <div
    class="price-sort-wrapper"
    @click="sort_price_reverse = !sort_price_reverse"
    :class="{ filterOn: sort_price }"
    >
    <div class="sort-btn" v-if="!sort_price_reverse">Low price to high price</div>
    <div class="sort-btn" v-if="sort_price_reverse">High price to low price</div>
  </div>

  <div class="filter-section">
    <div
      class="filter-btn"
      @click="filter_a_to_k = true;filter_l_to_z = true;"
      :class="{ filterOn: filter_a_to_k && filter_l_to_z }">ALL</div>
      
    <div
      class="filter-btn"
      @click="
        filter_a_to_k = true;
        filter_l_to_z = false;
      "
      :class="{ filterOn: filter_a_to_k }"
    >
      A-K
    </div>
    <div
      class="filter-btn"
      @click="
        filter_a_to_k = false;
        filter_l_to_z = true;
      "
      :class="{ filterOn: filter_l_to_z }"
    >
      L-Z
    </div>
  </div>

  <div class="class-list">
    <h1>Products</h1>
    <div class="product-wrapper" v-for="product in sorted_filtered_products">
      <h3>{{ product_names(product) }}</h3>
      <h5>{{ product.product_type }}</h5>
      <h5><span>$</span>{{ product.price }}</h5>
    </div>
  </div>
</template>

<style scoped>
.sort-btn-wrapper {
  display: flex;
}
.sort-btn {
  background-color: lightsalmon;
  padding: 10px;
  border: 2px whitesmoke double;
  margin: 5px;
  flex: 1;
  max-width: 200px;
  border-width: 10px;
}

.filter-section {
  display: flex;
  gap: 10px;
}

.filter-btn {
  background-color: lightgray;
  padding: 10px;
  border: 2px whitesmoke double;
  margin: 5px;
  flex: 1;
  max-width: 200px;
  border-width: 10px;
  cursor: pointer;
}

.filter-btn:hover {
  background-color: whitesmoke;
  border: 2px lightcoral double;
  border-width: 8px;
}

.filterOn {
  background-color: lightseagreen;
  padding: 10px;
  border: 2px whitesmoke double;
  margin: 5px;
  border-width: 10px;
}

.product-wrapper {
  background-color: #f7dbe9;
  padding: 20px;
  margin: 5px;
  border-radius: 10px;
}
</style>

<script>
export default {
  data() {
    return {
      product_array: [
        {
          product_name: "Ekos Tukuma",
          product_type: "Body Lotion",
          price: 50,
          id: 1,
        },
        {
          product_name: "Ekos Castanha",
          product_type: "Hand Cream",
          price: 20,
          id: 2,
        },
        {
          product_name: "Acai Frescor",
          product_type: "Fragance",
          price: 70,
          id: 3,
        },
        {
          product_name: "Natura Ilia Secreto",
          product_type: "Fragance",
          price: 70,
          id: 4,
        },
        {
          product_name: "Ucuuba Restorative",
          product_type: "Hand Cream",
          price: 10,
          id: 5,
        },
      ],
      sort_reverse: false,
      filter_a_to_k: true,
      filter_l_to_z: true,
      sort_price_reverse: false,
      sort_alph: false,
      sort_price: false,
    };
  },

  methods: {
    product_names(productObj) {
      return productObj.product_name;
    },
  },

  computed: {
    sorted_filtered_products() {
      return this.product_array
        .sort((productA, productB) => {
          let sort_multiplier = 1;
          if (this.sort_reverse) sort_multiplier = -1;

          if (productA.product_name > productB.product_name) return 1 * sort_multiplier;

          if (productA.product_name < productB.product_name) return -1 * sort_multiplier;

          return 0;
        })
        .filter(
          (product) =>
            (product.product_name[0] <= "K" && this.filter_a_to_k) ||
            (product.product_name[0] > "K" && this.filter_l_to_z)
        );
    },

    // sorted_price_products(){
    //   return this.product_array.sort(
    //     (priceA, priceB)=>{
    //       let sort_multiplier = 1;
    //       if(this.sort_price_reverse)
    //       sort_multiplier = -1;

    //       if(priceA.price > priceB.price)
    //       return 1 * sort_multiplier

    //       if (priceA.price < priceB.price)
    //       return -1 * sort_multiplier

    //       return 0;
    //     }
    //   )
    // }
  },
};
</script>
