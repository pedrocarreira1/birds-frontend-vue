<template>
  <div class="container d-flex align-items-center">
    <div class="row justify-content-center">
      <div class="col-md-6">
        <ImagesDescription />
      </div>
      <div class="col-md-6">
        <ImagesSlider />
      </div>
    </div>
  </div>
</template>

<script>

import ImagesDescription from "@/components/ImagesDescription.vue";
import ImagesSlider from "@/components/ImagesSlider.vue";

export default {
  name: 'App',
  components: {
    ImagesDescription,
    ImagesSlider
  }
}
</script>

<style>
  .container {
    min-height: 100vh;
    padding: 0;
    max-width: 1400px;
  }
</style>
