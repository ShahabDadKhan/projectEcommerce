<template>
  <v-hover v-slot="{ hover }">
    <v-card class="mx-auto" height="100%" max-width="350" tile>
      <v-img :src="imagePath" height="500px">
        <v-expand-transition>
          <div
            v-if="hover"
            class="d-flex transition-fast-in-fast-out red darken-2 v-card--reveal white--text"
            style="height: 5%;"
          >
            VIEW DETAILS
          </div>
        </v-expand-transition>
      </v-img>

      <v-card-title class="subtitle-1 font-weight-light mb-1">
        {{ product.name }}
      </v-card-title>

      <v-card-subtitle class="d-flex ">
        <div
          v-show="product.selling_price !== product.price"
          class="sellingPrice mr-3"
          style="  text-decoration: line-through;"
        >
          Rs. {{ product.price }}
        </div>
        <div class="price black--text font-weight-light">
          Rs. {{ product.selling_price }}
        </div>
        <div
          v-show="product.selling_price !== product.price"
          class="discount ml-3 red--text font-weight-black"
        >
          -{{ discount }}%
        </div>
      </v-card-subtitle>
      <v-card-subtitle> Size - {{ size }} </v-card-subtitle>
    </v-card>
  </v-hover>
</template>

<script>
export default {
  data: () => ({
    productSize: [],
  }),
  // Receiving the information from TheHome & rendring into card
  props: {
    product: {
      required: true,
    },
  },

  computed: {
    // fethcing the images of the products
    imagePath() {
      return this.product.image;
    },

    // calculating discount before displaying it
    discount() {
      return Math.trunc(
        ((this.product.price - this.product.selling_price) /
          this.product.price) *
          100
      );
    },
    size() {
      // eslint-disable-next-line vue/no-side-effects-in-computed-properties
      return (this.productSize = JSON.parse(
        this.product.size.replace(/\]\s*,\s*\[/g, ", ")
      ));
    },
  },
};
</script>

<style lang="scss" scoped>
.v-image:hover {
  cursor: pointer;
}

.v-card--reveal {
  align-items: center;
  bottom: 0;
  justify-content: center;
  position: absolute;
  width: 100%;
}

.v-card {
  box-shadow: none !important;

  &:hover {
    box-shadow: 0px 1px 1px -2px rgb(0 0 0 / 20%),
      0px 1px 1px 0px rgb(0 0 0 / 14%), 0px 1px 1px 0px rgb(0 0 0 / 12%) !important;
  }
}

.v-card__title:hover {
  cursor: pointer;
  text-decoration: underline;
}

.sellingPrice {
  color: lightgrey;
}

// .v-card__subtitle:last-child {
//   opacity: 0;

//   &:hover {
//     opacity: 1;
//     // visibility: visible !important;
//   }
// }
</style>
