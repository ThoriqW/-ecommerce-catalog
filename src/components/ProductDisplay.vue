<template>
  <div>
    <div v-if="loading" class="container-loader">
      <!-- Loader content -->
      <div class="loader"></div>
    </div>
    <div v-else>
      <div
        v-if="products"
        class="container"
        :class="{
          'bg-men': this.products.category === men,
          'bg-women': this.products.category === women,
        }"
      >
        <div class="container-product">
          <div class="flex">
            <div class="flex-left">
              <img class="image" :src="`${products.image}`" alt="product" />
            </div>
            <div class="flex-right">
              <h1
                class="title-product"
                :class="{
                  'color-text-men': this.products.category === men,
                  'color-text-women': this.products.category === women,
                }"
              >
                {{ products.title }}
              </h1>
              <div>
                <p class="category-product">{{ products.category }}</p>
              </div>
              <hr />
              <p class="description">{{ products.description }}</p>
              <div>
                <hr />
                <h1
                  class="price"
                  :class="{
                    'color-text-men': this.products.category === men,
                    'color-text-women': this.products.category === women,
                  }"
                >
                  ${{ products.price }}
                </h1>
                <div>
                  <button
                    class="btn buy"
                    :class="{
                      'bg-button-buy-men': this.products.category === men,
                      'bg-button-buy-women': this.products.category === women,
                    }"
                  >
                    Buy Now
                  </button>
                  <button
                    @click.prevent="nextProduct"
                    class="btn next"
                    :class="{
                      'bg-button-next-men': this.products.category === men,
                      'bg-button-next-women': this.products.category === women,
                    }"
                  >
                    Next Product
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div v-if="!products" class="container bg-gray">
        <div class="container-product">
          <div class="no-product">
            <div>
              <p>This product is unavailable tho show</p>
              <button @click.prevent="nextProduct" class="btn next not-show">
                Next Product
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ProductDisplay",
  data() {
    return {
      loading: true, // Loading state variable
      products: {},
      index: 1,
      men: "men's clothing",
      women: "women's clothing",
    };
  },
  mounted() {
    this.fetchData(this.index);
  },
  methods: {
    fetchData(index) {
      this.loading = true; // Show loader before fetching data
      fetch(`https://fakestoreapi.com/products/${index}`)
        .then((response) => response.json())
        .then((data) => {
          // Handle the fetched data here
          if (
            data.category === "men's clothing" ||
            data.category === "women's clothing"
          ) {
            this.products = data;
            console.log(this.products);
          } else {
            console.log("this");
            this.products = false;
          }
        })
        .catch((error) => {
          // Handle any errors here
          console.log(error);
        })
        .finally(() => {
          this.loading = false; // Hide loader after API call is complete
        });
    },

    nextProduct() {
      if (this.index < 20) {
        this.index++;
      } else {
        this.index = 1;
      }
      this.fetchData(this.index);
    },
  },
};
</script>

<style scoped></style>
