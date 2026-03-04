<script setup>
import CardProduct from '@/components/CardProduct.vue';
import { ref, onMounted } from 'vue';
import { useFetch } from '@/composables/fetch.js';

const products = ref([]);

onMounted(async () => {
  let url = "https://dummyjson.com/products";
  let {data, error} = await useFetch(url);

  if(error.value){
    return alert("Error al intertar conectarse a la API");
  };
  //MANIPULACIÓN DE DATOS
  let listProducts = data.value.products;

  products.value = listProducts.map(p => {
    let {id, title, description, brand, price, sku, thumbnail, images} = p;
    let objProduct = {id, title, description, brand, price, sku, thumbnail, images};

    return objProduct;
  });
  console.log(products.value);
});
</script>

<template>
  <div>
    <header>
      <h1 class="text-center">Nuestros Pruductos</h1>
    </header>
  </div>

  <main class="container">
    <section>
      <h2>Todos los productos disponibles</h2>
      <div class="row g-2 justify-content-evenly row-cols-1 row-cols-sm-2 row-cols-md-3 row-cols-lg-4" v-if="products.length">
        <div class="col" v-for="product in products" :key="product.id">
          <CardProduct :product/>
        </div>
      </div>
    </section>
  </main>

</template>

<style scoped lang="css">
</style>
