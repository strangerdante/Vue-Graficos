<script setup>
import { ref } from "vue";
import GraficoDona from "./components/GraficoDona.vue";
import GraficoLinea from "./components/GraficoLinea.vue";
import GraficoLinea2 from "./components/GraficoLinea2.vue";
import GraficoProgreso from "./components/GraficoProgreso.vue";
import Slider from "./components/Slider.vue";
import GraficosTickets from "./components/GraficosTickets.vue";
import GraficoBarra from "./components/GraficoBarra.vue";
import AppNavbar from "./components/AppNavbar.vue";
import AppSidebar from "./components/AppSidebar.vue";

// Estado para controlar el sidebar
const sidebarOpen = ref(false);

// Función para alternar el sidebar
const toggleSidebar = () => {
  sidebarOpen.value = !sidebarOpen.value;
};

// Función para cerrar el sidebar
const closeSidebar = () => {
  sidebarOpen.value = false;
};
</script>

<template>
  <div class="min-h-screen bg-gray-900">
    <!-- Navbar superior -->
    <AppNavbar @toggle-sidebar="toggleSidebar" />

    <!-- Contenido principal -->
    <div class="relative">
      <!-- Dashboard con gráficos -->
      <div class="m-4 grid grid-cols-1 gap-4 sm:grid-cols-4">
        <div
          class="flex-col rounded-lg bg-gray-700 sm:col-span-2 sm:row-span-2"
        >
          <GraficosTickets />
        </div>

        <div class="h-36 rounded-lg bg-gray-700 sm:col-start-1 sm:row-start-3">
          <GraficoProgreso />
        </div>
        <div
          class="flex h-36 justify-center rounded-lg bg-gray-700 sm:col-start-2 sm:row-start-3"
        >
          <GraficoLinea2 />
        </div>
        <div
          class="h-36 flex-col justify-center rounded-lg bg-gray-700 p-4 sm:col-start-1 sm:row-start-4"
        >
          <div class="flex">
            <p class="font-bold text-white">$456,623</p>
            <p class="ml-auto text-gray-400">Mensualmente</p>
          </div>
          <GraficoLinea class="p-2" />
        </div>
        <div
          class="flex h-36 justify-center rounded-lg bg-gray-700 sm:col-start-2 sm:row-start-4"
        >
          <GraficoDona />
        </div>
        <div
          class="flex h-[300px] justify-center rounded-lg bg-gradient-to-r from-teal-400 to-teal-700 sm:col-span-2 sm:col-start-3 sm:row-start-1"
        >
          <GraficoBarra />
        </div>
        <div
          class="h-[300px] rounded-lg bg-gray-700 sm:col-span-2 sm:col-start-3 sm:row-span-3 sm:row-start-2 sm:h-[420px]"
        >
          <h1 class="mb-2 px-4 pt-4 text-xl font-semibold text-white">
            Galerías de eventos
          </h1>
          <Slider />
        </div>
      </div>
    </div>

    <!-- Sidebar -->
    <AppSidebar :is-open="sidebarOpen" @close="closeSidebar" />

    <!-- Overlay para cerrar el sidebar en móvil -->
    <div
      v-if="sidebarOpen"
      @click="closeSidebar"
      class="fixed inset-0 z-[9998] bg-black bg-opacity-50 transition-opacity duration-300"
    ></div>
  </div>
</template>
