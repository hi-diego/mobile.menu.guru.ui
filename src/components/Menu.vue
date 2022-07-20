<template lang="pug">
v-container(class="main-menu")
  .menu-item(v-for="product in products")
    v-row.limit-h(style="max-height: 65%")
      v-img.index(height="400", :src="`/img/products/${product.image}`")
    .title.d-flex.flex-column.pa-5
      p.font-weight-light.invert--text.mb-0 {{ product.category }}
      h1.text-h3.font-weight-light.invert--text {{ product.name }}
      .icons.d-flex.my-5
        small.mr-10.d-flex
          v-icon.invert--text mdi-clock-outline
          span.mx-1.invert--text 30 min
        small.mr-10.d-flex
          v-icon.invert--text mdi-heart
          span.mx-1.invert--text 30
    v-row.index.py-5
      .blurry(:style="{ 'background-image': `url(/img/products/${product.image})` }")
      v-card.index.mx-auto(style="border-radius: 20px; background: transparent")
        v-card-title {{ product.name  }}
        v-card-text
          v-row.mx-0(align='center')
            v-rating(:value='4.5' color='amber' dense='' half-increments='' readonly='' size='14')
            .grey--text.ms-4
              | 4.5 (413)
          .my-4.text-subtitle-1
            | {{ product.price }}$ &bull; {{ product.category }}
          div
            | {{ product.description }}
        v-divider.mx-4
        v-card-actions.flex.justify-end
          v-btn(color='darken-5' text='' @click="order(product)") Ordenar
  v-dialog(v-model="billDialog", scrollable, fullscreen, transition="dialog-bottom-transition")
    template(v-slot:activator="{ on, attrs }")
      v-btn.upfront.secondary(fab, dark, small, bottom, fixed, left, color="primary", v-bind="attrs", v-on="on")
        v-icon mdi-menu
    v-card.bill-card.secondary
      v-card-title.d-flex.fill-width.justify-space-between
        | Cuenta
        v-btn(icon, @click="billDialog = false")
          v-icon mdi-close
      v-card-subtitle.pb-0 Mesa 1
      v-card-text.pa-2.list
        v-list-item(v-for="(product, i) in orders", :key="i")
          v-list-item-content
            v-list-item-title {{ product.name }} ({{ product.category }}) x 1
            v-list-item-subtitle.d-flex.justify-end.bill-item
              p {{ subTotal }}$
      v-card-actions(v-if="bill")
        v-list-item
          v-list-item-content
            v-list-item-title
              strong TOTAL
            v-list-item-subtitle.d-flex.justify-end.bill-item
              strong {{ bill.calculatedTotal }}$
</template>

<style>
.upfront {
  z-index: 999 !important;
}
.bill-item {
  border-bottom: 1px dotted white !important;
  /*line-height: 0.8 !important;*/
}
.bill-item p {
  margin: 0px !important;
}
.order-btn {
  position: absolute;
  right: 0px;
}
.v-dialog--fullscreen {
  top: 30% !important;
  border-radius: 0% !important;
  border-top-left-radius: 20px !important;
  border-top-right-radius: 20px !important;
  height: 70%;
}
div.bill-card.secondary {
  background: linear-gradient(345deg, rgba(161,28,28,1) 0%, rgba(235,19,19,1) 100%) !important;
}
div.bill-card.secondary * {
  color: white !important;
}
</style>

<style>
.index {
  z-index: 5;
}
.main-menu {
  min-height: 100%;
  /*background: rgb(18,18,18);*/
  /*background: linear-gradient(7deg, rgba(18,18,18,1) 0%, rgba(63,46,46,1) 35%, rgba(38,45,73,1) 100%);*/
}
.menu-item {
  height: 100vh;
  position: relative;
  content: '';
}

.blurry {
  height: 100vh;
  width: 100vw;
  content: '';
  position: absolute;
  top: 0%;
  display: flex;
  background-repeat: round;
  filter: blur(37px);
}

.title {
  z-index: 5;
  position: absolute;
  top: 0px;
}
.invert--text {
  filter: invert(1) grayscale(1);
  mix-blend-mode: difference;
}
</style>
<script>
import axios from 'axios'
const products = require('../assets/products.json')
export default {
  //
  data: function () {
    return {
      products,
      orders: [],
      billDialog: false,
      publicPath: process.env.BASE_URL
    }
  },
  computed: {
    subTotal () {
      return this.orders.reduce((a, c, n) => a + c.price, 0)
    }
  },
  methods: {
    async order (product) {
      try {
        await axios.post('orders', product)
      } catch (err) {
        console.err(err)
      }
      this.orders.push(product)
    }
  }
}
</script>
