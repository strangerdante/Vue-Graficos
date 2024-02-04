<template>
  <swiper-container
    class="rounded-xl"
    navigation="true"
    pagination="true"
    scrollbar="true"
  >
    <swiper-slide
      ><img src="https://picsum.photos/1200/400?random=1"
    /></swiper-slide>
    <swiper-slide
      ><img src="https://picsum.photos/1200/400?random=2"
    /></swiper-slide>
    <swiper-slide
      ><img src="https://picsum.photos/1200/400?random=3"
    /></swiper-slide>
  </swiper-container>
</template>

<script>
import { register } from "swiper/element/bundle";
// register Swiper custom elements
register();
</script>

<style></style>
