<script setup>
import { ref, computed } from 'vue'
import { useDisplay } from 'vuetify'
const display = useDisplay();
const isMobile = computed(() => display.smAndDown.value)
/* ------------------------------------------------------------------
 * Demo-only data.
 * Replace with your API call or Vuex/Pinia store in production.
 * -----------------------------------------------------------------*/
const bannerImage =
    'https://source.unsplash.com/1600x400/?beauty,cosmetics,makeup'

const featuredProducts = ref([
  { id: 1, name: 'Luxury Facial Serum',  price: 'R$ 129,90', keyword: 'serum,skincare' },
  { id: 2, name: 'Velvet Matte Lipstick', price: 'R$ 59,90',  keyword: 'lipstick,makeup' },
  { id: 3, name: 'Nourishing Hair Oil',  price: 'R$ 89,00',  keyword: 'hair,oil' },
  { id: 3, name: 'Nourishing Hair Oil',  price: 'R$ 89,00',  keyword: 'hair,oil' },
  { id: 3, name: 'Nourishing Hair Oil',  price: 'R$ 89,00',  keyword: 'hair,oil' },
])
const getImage = (keyword) =>
    `https://source.unsplash.com/300x200/?${encodeURIComponent(keyword || 'beauty')}`

const otherProducts = ref([
  { id: 4,  name: 'Hydrating Shampoo',     price: 'R$ 39,90',  keyword: 'shampoo,hair' },
  { id: 5,  name: 'Body Lotion Delight',   price: 'R$ 29,90',  keyword: 'body,lotion' },
  { id: 6,  name: 'Perfume Essence',       price: 'R$ 149,00', keyword: 'perfume,fragrance' },
  { id: 7,  name: 'SPF 50 Sun Gel',        price: 'R$ 69,90',  keyword: 'sunscreen' },
  { id: 8,  name: 'Cuticle Revitalizer',   price: 'R$ 24,99',  keyword: 'nail' },
  { id: 9,  name: 'Glow Highlighter',      price: 'R$ 64,90',  keyword: 'highlighter' },
  { id: 10, name: 'Revitalizing Mask',     price: 'R$ 79,90',  keyword: 'mask,skincare' },
])

/* Helper to get Unsplash image */
const img = (k) => `https://source.unsplash.com/300x200/?${encodeURIComponent(k)}`

/* Combine lists so the template can v-for just once */
const products = computed(() => [...featuredProducts.value, ...otherProducts.value])
</script>

<template>
  <v-container class="pa-0" fluid>
    <!-- Full-width banner -->
    <div class="store_main">
      <v-img
          :src="bannerImage"
          height="280"
          cover
          class="mb-4"
      >
        <template #default>
          <div class="d-flex flex-column align-center justify-center fill-height my-banner">
            <h1 class="white--text font-weight-bold display-1 text-center text-shadow">
              Beleza Shop Online
            </h1>
            <p class="white--text subtitle-2 text-center text-shadow">
              Tudo o que você precisa em cuidados de beleza, em um só lugar.
            </p>
          </div>
        </template>
      </v-img>
      <div class="destack">
        <h2 class="text-center font-weight-bold mb-3 px-2">Destaques</h2>
        <v-slide-group
            class="mb-4 px-2 featured-group"
            :show-arrows="$vuetify.display.width > 480"
        >
          <v-slide-group-item
              v-for="item in featuredProducts"
              :key="item.id"
              class="slide-item px-1"
          >
            <v-card class="featured-card" :class="isMobile ? 'mx-1' : 'ml-16 mx-2'" elevation="6">
              <v-img :src="getImage(item.keyword)" height="120" cover rounded="lg" />
              <v-card-text class="text-center py-3">
                <div class="text-body-1 font-weight-medium">{{ item.name }}</div>
                <div class="text-subtitle-2 text-primary font-weight-bold">
                  {{ item.price }}
                </div>
              </v-card-text>
              <v-card-actions class="justify-center pb-3 pt-0">
                <v-btn color="primary" size="small" variant="flat">Comprar</v-btn>
              </v-card-actions>
            </v-card>
          </v-slide-group-item>
        </v-slide-group>
      </div>

      <!-- Scrollable product column -->
      <div class="product-list px-2">
        <v-container fluid="fluid">
          <h2 class="mt-7 text-center">Veja nossa linha completa de produtos:</h2>
          <v-row dense class="mt-7">
            <!-- Display products in a single column (full-width on mobile, 6 cols MD, 4 cols LG)  -->
            <v-col
                v-for="(product, idx) in products"
                :key="product.id"
                cols="12"
                md="6"
                lg="4"
            >
              <v-card
                  :elevation="idx < 3 ? 8 : 3"
                  class="product-card"
              >
                <!-- Product image -->
                <v-img :src="img(product.keyword)" height="160" cover />
                <v-card-text class="py-4 text-center">
                  <!-- Featured badge -->
                  <v-chip
                      v-if="idx < 3"
                      color="pink-darken-1"
                      size="small"
                      class="mb-2 text-white"
                  >
                    Destaque
                  </v-chip>

                  <div class="text-body-1 font-weight-medium">{{ product.name }}</div>
                  <div class="text-h6 font-weight-bold text-pink-darken-2">
                    {{ product.price }}
                  </div>
                </v-card-text>

                <v-card-actions class="justify-center pb-4 pt-0">
                  <v-btn
                      color="pink-darken-1"
                      variant="elevated"
                      rounded="pill"
                      size="small"
                  >
                    Comprar
                  </v-btn>
                </v-card-actions>
              </v-card>
            </v-col>
          </v-row>
        </v-container>
      </div>
    </div>

  </v-container>
</template>

<style scoped lang="scss">
.store_main{
  overflow-y: auto;
  scrollbar-width: none;
  .my-banner {
    background: rgba(0, 0, 0, 0.35);
    padding: 20px;
    border-radius: 8px;
  }

  .text-shadow {
    text-shadow: 0 2px 8px #0008;
  }

  /* ---------------------------------------------------------------
     Makes the product area scroll while the banner stays fixed.
     280px banner + 32px (margin + paddings) ≈ 312px
     -------------------------------------------------------------- */
  .product-list {
    height: calc(100vh - 312px);
           /* Firefox */
  }
  .product-list::-webkit-scrollbar { /* Chrome, Safari */
    display: none;
  }

  /* Card aesthetics */
  .product-card {
    border-radius: 14px;
    transition: transform 0.25s;
  }
  .product-card:hover {
    transform: translateY(-3px);
  }
}

@media (max-width: 768px) {
  .product-list {
    height: calc(100vh - 280px);
  }
}
</style>