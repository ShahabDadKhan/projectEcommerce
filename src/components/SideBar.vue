<template>
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
              <v-expansion-panel v-for="filter in filters" :key="filter">
                <v-expansion-panel-header>
                  {{ filter.filter_lable }}
                </v-expansion-panel-header>
                <v-expansion-panel-content
                  v-for="option in filter.options"
                  :key="option.total"
                >
                  <div class="d-flex flex-row align-center">
                    <v-btn tile text @click="applyFilter(filter, option)">
                      <div
                        class="filterBtn"
                        :style="{ background: option.value }"
                      ></div>
                      <div class="filterBtn-title">
                        {{ option.value }} <span> ({{ option.total }}) </span>
                      </div>
                    </v-btn>
                  </div>
                </v-expansion-panel-content>
              </v-expansion-panel>
            </v-expansion-panels>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
  </v-card>
</template>

<script>
export default {
  props: {
    filters: {
      required: true,
    },
  },
  data() {
    return {};
  },

  methods: {
    applyFilter(filter, option) {
      if (filter.filter_lable === "Colour") {
        // filtering the products by Colours
        console.log("Hello, I'm a Colours");

        return (
          "https://pim.wforwoman.com/pim/pimresponse.php/?service=category&store=1&url_key=top-wear-kurtas&page=1&count=20&sort_by=&sort_dir=desc&filter=" +
          "color-" +
          option.value
        );
        // async fetchProducts() {
        //   const baseURL =
        //     "https://pim.wforwoman.com/pim/pimresponse.php/?service=category&store=1&url_key=top-wear-kurtas&page=1&count=20&sort_by=&sort_dir=desc&filter=";
        //   const response = await this.$http.get(baseURL);
        //   this.allProducts = response.data.result.products;
        //   console.log(this.allProducts);
        // },
      }
      if (filter.filter_lable === "Price") {
        // filtering the products by Price
        console.log("Hello, I'm a Price");

        return (
          "https://pim.wforwoman.com/pim/pimresponse.php/?service=category&store=1&url_key=top-wear-kurtas&page=1&count=20&sort_by=&sort_dir=desc&filter=" +
          "selling_price-" +
          option.value
        );
      }
      if (filter.filter_lable === "Discount") {
        // filtering the products by Discount
        console.log("Hello, I'm a Discount");

        return (
          "https://pim.wforwoman.com/pim/pimresponse.php/?service=category&store=1&url_key=top-wear-kurtas&page=1&count=20&sort_by=&sort_dir=desc&filter=" +
          "discount-" +
          option.values
        );
      }
    },
  },
};
</script>

<style lang="scss" scoped>
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
