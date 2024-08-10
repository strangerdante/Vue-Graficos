<template>
  <section>
    <div class="mx-auto transition duration-300 ease-in-out sm:px-6">
      <swiper
        :slides-per-view="1"
        :space-between="30"
        :navigation="{
          nextEl: '.swiper-button-next',
          prevEl: '.swiper-button-prev',
          hideOnMobile: true,
        }"
        :pagination="{ clickable: true }"
        :modules="modules"
        :loop="true"
        :grab-cursor="false"
        :autoplay="{
          delay: 3000,
          disableOnInteraction: false,
        }"
        :effect="'fade'"
        :fade-effect="{ crossFade: true }"
        class="custom-swiper overflow-hidden sm:rounded-lg"
      >
        <swiper-slide v-for="(slide, index) in slides" :key="index">
          <div class="relative">
            <img
              :src="slide.image"
              :alt="`Slide ${index + 1}`"
              class="h-[240px] w-full object-cover sm:h-[330px] sm:rounded-lg"
            />
            <div
              v-if="slide.titulo || slide.descripcion || slide.textoBoton"
              class="absolute inset-0 flex flex-col items-center justify-evenly bg-black bg-opacity-50 text-white"
            >
              <h3
                v-if="slide.titulo"
                class="mb-2 text-xl font-bold sm:mb-4 sm:text-2xl"
              >
                {{ slide.titulo }}
              </h3>
              <p
                v-if="slide.descripcion"
                class="mb-4 px-4 text-sm sm:mb-6 sm:px-24 sm:text-xl"
              >
                {{ slide.descripcion }}
              </p>
              <button
                v-if="slide.textoBoton"
                class="rounded bg-teal-500 px-4 py-2 text-sm font-bold text-white hover:bg-teal-600 sm:text-base"
                @click="handleButtonClick(slide.linkBoton)"
              >
                {{ slide.textoBoton }}
              </button>
            </div>
          </div>
        </swiper-slide>
        <div class="swiper-button-next custom-swiper-button">
          <i class="fas fa-chevron-right"></i>
        </div>
        <div class="swiper-button-prev custom-swiper-button">
          <i class="fas fa-chevron-left"></i>
        </div>
      </swiper>
    </div>
  </section>
</template>

<script>
import { Swiper, SwiperSlide } from "swiper/vue";
import { Navigation, Pagination, Autoplay, EffectFade } from "swiper/modules";
import "swiper/css";
import "swiper/css/navigation";
import "swiper/css/pagination";
import "swiper/css/autoplay";
import "swiper/css/effect-fade";

export default {
  components: {
    Swiper,
    SwiperSlide,
  },
  data() {
    return {
      modules: [Navigation, Pagination, Autoplay, EffectFade],
      slides: [
        {
          image: "https://picsum.photos/1200/400?random=1",
          titulo: "Ejemplo 1",
          descripcion: "descripción",
          textoBoton: "Ver detalles",
          linkBoton: "/pagina1",
        },
        {
          image: "https://picsum.photos/1200/400?random=2",
          titulo: "Ejemplo 2",
          descripcion: "descripción",
          textoBoton: "Ver detalles",
          linkBoton: "/pagina2",
        },
        {
          image: "https://picsum.photos/1200/400?random=3",
          titulo: "Ejemplo 3",
          descripcion: "descripción",
          textoBoton: "Ver detalles",
          linkBoton: "/pagina2",
        },
      ],
    };
  },
  methods: {
    handleButtonClick(link) {
      console.log(`Navegando a: ${link}`);
      // this.$router.push(link); // Descomenta esta línea si estás usando vue-router
    },
  },
};
</script>

<style lang="postcss">
/* Estilos para los paginadores */
:root {
  --swiper-theme-color: #14b8a6 !important; /* teal-500 */
}

/* Estilos para las flechas de navegación */
.custom-swiper-button {
  color: #14b8a6 !important; /* teal-500 */
}

/* Opcional: Estilo para el hover de las flechas */
.custom-swiper-button:hover {
  color: #0d9488 !important; /* teal-600 para el hover */
}

/* Asegúrate de que las flechas sean visibles */
.swiper-button-next::after,
.swiper-button-prev::after {
  font-size: 24px;
}
</style>
