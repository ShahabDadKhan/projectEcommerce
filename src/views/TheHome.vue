<template>
  <v-container fluid>
    <v-row>
      <!-- SideBar -->
      <v-col sm="3">
        <v-card height="auto" width="100%" class="mx-auto">
          <v-navigation-drawer width="100%" permanent>
            <v-list-item>
              <v-list-item-content>
                <v-list-item-title class="text-h6">
                  FILTER
                </v-list-item-title>
              </v-list-item-content>
            </v-list-item>

            <v-divider></v-divider>

            <v-list dense nav>
              <v-list-item>
                <v-list-item-content>
                  <v-expansion-panels>
                    <v-expansion-panel
                      v-for="filter in filters"
                      :key="filter.options.value"
                    >
                      <v-expansion-panel-header>
                        {{ filter.filter_lable }}
                      </v-expansion-panel-header>
                      <v-expansion-panel-content
                        v-for="option in filter.options"
                        :key="option.value_key"
                      >
                        <div class="d-flex flex-row align-center">
                          <v-btn-toggle multiple>
                            <v-btn
                              tile
                              text
                              active-class
                              m
                              @click="applyFilter(filter, option)"
                            >
                              <div
                                class="filterBtn"
                                :style="{ background: option.value }"
                              ></div>
                              <div class="filterBtn-title">
                                {{ option.value }}
                                <span> ({{ option.total }}) </span>
                              </div>
                            </v-btn>
                          </v-btn-toggle>
                        </div>
                      </v-expansion-panel-content>
                    </v-expansion-panel>
                  </v-expansion-panels>
                </v-list-item-content>
              </v-list-item>
            </v-list>
          </v-navigation-drawer>
        </v-card>
      </v-col>
      <v-col sm="9" class="d-flex flex-row">
        <v-row>
          <!-- Displaying Progress circle untill products load -->
          <v-col align-self="center" class="d-flex justify-center" sm="12">
            <v-progress-circular
              class="pa-12 mt-15"
              v-show="loading"
              :size="70"
              :width="7"
              indeterminate
              color="purple"
            ></v-progress-circular>
          </v-col>

          <!-- The main screen where user see the products -->

          <v-col
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
import TheCard from "../components/TheCard.vue";
export default {
  data() {
    return {
      loading: null,
      allProducts: [],
      filters: [],
      selectedFilters: "",
    };
  },
  components: {
    TheCard,
  },
  mounted() {
    this.fetchProducts();
    this.fetchFilters();
  },
  watch: {
    // Keeping an eye on fetchProducts so as to apply filters as the soon as there is a change in params
    selectedFilters: {
      handler() {
        this.fetchProducts();
      },
    },
  },
  methods: {
    // fetching the products
    async fetchProducts() {
      this.loading = true;
      const baseURL =
        "https://pim.wforwoman.com/pim/pimresponse.php/?service=category&store=1&url_key=top-wear-kurtas&page=1&count=400&sort_by=&sort_dir=desc&filter=";
      const response = await this.$http.get(baseURL, {
        params: {
          filter: this.selectedFilters,
        },
      });
      this.allProducts = response.data.result.products;
      this.loading = false;
      console.log(this.allProducts);
    },

    // fetching the filters to use them dynamically on sidebar
    async fetchFilters() {
      const baseURL =
        "https://pim.wforwoman.com/pim/pimresponse.php/?service=category&store=1&url_key=top-wear-kurtas&page=1&count=20&sort_by=&sort_dir=desc&filter=";
      const response = await this.$http.get(baseURL);
      this.filters = response.data.result.filters;
      console.log("These are fiters", this.filters);
    },

    // Applying filters depending upon what filter is being chosen
    applyFilter(filter, option) {
      console.log("Filter wala hai ye", `color-${option.value}`);

      if (filter.filter_lable === "Colour") {
        // filtering products by Colours
        console.log("Hello, I'm a Colours");
        this.selectedFilters =
          this.selectedFilters === ""
            ? `color-${option.value}`
            : `${this.selectedFilters},color-${option.value}`;
      }

      if (filter.filter_lable === "Price") {
        // filtering products by Price
        console.log("Hello, I'm a Price");
        this.selectedFilters =
          this.selectedFilters === ""
            ? `selling_price-${option.value}`
            : `${this.selectedFilters},selling_price-${option.value}`;
      }
      if (filter.filter_lable === "Discount") {
        // filtering products by Discount
        console.log("Hello, I'm a Discount");
        this.selectedFilters =
          this.selectedFilters === ""
            ? `discount-${option.value}`
            : `${this.selectedFilters},discount-${option.value}`;
      }
      if (filter.filter_lable === "Size") {
        // filtering products by Size
        console.log("Hello, I'm a Size");
        this.selectedFilters =
          this.selectedFilters === ""
            ? `size-${option.value}`
            : `${this.selectedFilters},size-${option.value}`;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.row {
  height: 100%;
}

// Card styling
.v-card {
  box-shadow: none !important;
}

span {
  margin-left: 10px;
  font: 100 10px sans-serif;
}

::v-deep .v-expansion-panel-content__wrap {
  padding: 0px 10px;
}

.v-expansion-panel--active {
  height: 200px;
  overflow: scroll;
}

.v-btn {
  width: 100%;
  display: flex;
  flex-direction: row;
  justify-content: left;
  &:hover,
  :focus {
    border-color: red !important;
  }
}

.filterBtn {
  height: 20px;
  width: 20px;
  border: 1px solid black;
  margin-right: 15px;

  &-title {
    display: flex;
    align-items: center;
  }
}
</style>
