<template>
<div class="col-md-4" v-for="post in posts" :key="post.id">
  <div class="card mb-4 shadow-sm">
    <img :src="product.imageUrl" class="card-img-top post-image" />
    <div class="card-body">
      <h5 class="card-title text-left">{{ post.title }}</h5>
      <div class="row">
        <router-link
          type="button"
          class="btn btn-primary btn-lg"
          :to="'/details/' + post.id"
        >Details</router-link>
      </div>
    </div>
  </div>
</div>
</template>

<script>
export default {
    name: "ProductCard",
    props: ["blog"]
};
</script>

<style scoped>
.card .product-image {
  height: 300px;
}
</style>