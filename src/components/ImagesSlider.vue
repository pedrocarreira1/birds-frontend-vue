<template>
  <div class="slideshow-container" v-if="images.length > 0">
    <!-- Display the current image -->
    <img :src="images[currentIndex]" alt="Slideshow Image" class="slideshow-image" />
    <!-- Navigation buttons -->
    <button @click="prevSlide" class="prev-button">
      <img src="../assets/arrow-left-solid.svg" alt="Previous" class="arrow-icon" />
    </button>
    <button @click="nextSlide" class="next-button">
      <img src="../assets/arrow-right-solid.svg" alt="Next" class="arrow-icon" />
    </button>
    <img src="../assets/secondary-image-1.webp" class="secondary-image" />
  </div>
  <div v-else>
    <p>Loading images...</p>
  </div>
  <!-- Display a secondary image -->
</template>

<script>
import {onMounted, ref} from "vue";

export default {
  setup() {
    const images = ref([]);
    const currentIndex = ref(0);

    // Fetch images from the Laravel API
    const fetchImages = async () => {
      try {
        const response = await fetch("http://localhost:3000/api/images");
        images.value = await response.json();
      } catch (error) {
        console.error("Error fetching images:", error);
      }
    };

    // Show the next image
    const nextSlide = () => {
      if (images.value.length === 0) return;
      currentIndex.value = (currentIndex.value + 1) % images.value.length;
    };

    // Show the previous image
    const prevSlide = () => {
      if (images.value.length === 0) return;
      currentIndex.value = (currentIndex.value - 1 + images.value.length) % images.value.length;
    };

    // Fetch images when the component is mounted
    onMounted(() => {
      fetchImages();
    });

    return {
      images,
      currentIndex,
      nextSlide,
      prevSlide,
    };
  }
};
</script>

<style scoped>
.slideshow-container {
  position: relative;
  width: 100%;
  height: 500px;
  margin: auto;
}

.slideshow-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.secondary-image {
  position: relative;
  top: -350px;
  right: -180px;
  width: 80%;
  height: 80%;
  z-index: -1;
}

button {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  padding: 10px;
  background-color: rgb(255, 255, 255, 0.5);
  border: none;
  cursor: pointer;
  z-index: 1;
}

.prev-button {
  left: 10px;
}

.next-button {
  right: 10px;
}

.arrow-icon {
  width: 30px;
  height: 30px;
}
</style>
