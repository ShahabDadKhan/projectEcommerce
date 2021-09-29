<template>
  <v-container fluid>
    <v-row>
      <v-col sm="3">
        <side-bar :filters="filters" />
      </v-col>
      <v-col sm="9" class="d-flex flex-row">
        <v-row
          ><v-col
            cols="12"
            sm="4"
            md="3"
            lg="3"
            class="pa-2"
            v-for="product in allProducts"
            :key="product.id_product"
          >
            <!-- Using the card component to display the products & passing the information through props using unique product id -->
            <the-card :product="product" />
          </v-col>
        </v-row>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import SideBar from "../components/SideBar.vue";
import TheCard from "../components/TheCard.vue";
export default {
  data() {
    return {
      allProducts: [],
      filters: [],
    };
  },
  components: { TheCard, SideBar },
  mounted() {
    this.fetchProducts();
    this.fetchFilters();
  },
  methods: {
    // fetching the products
    async fetchProducts() {
      const baseURL =
        "https://pim.wforwoman.com/pim/pimresponse.php/?service=category&store=1&url_key=top-wear-kurtas&page=1&count=20&sort_by=&sort_dir=desc&filter=";
      const response = await this.$http.get(baseURL);
      this.allProducts = response.data.result.products;
      console.log(this.allProducts);
    },
    // fetching the filters
    async fetchFilters() {
      const baseURL =
        "https://pim.wforwoman.com/pim/pimresponse.php/?service=category&store=1&url_key=top-wear-kurtas&page=1&count=20&sort_by=&sort_dir=desc&filter=";
      const response = await this.$http.get(baseURL);
      this.filters = response.data.result.filters;
      console.log(this.filters);
    },
  },
};
</script>

<style lang="scss" scoped>
.row {
  height: 100vh;
}
</style>
