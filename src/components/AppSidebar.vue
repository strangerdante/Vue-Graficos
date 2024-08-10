<template>
  <!-- Sidebar -->
  <div
    :class="[
      'fixed inset-y-0 right-0 z-[9999] w-80 bg-gray-800 shadow-xl transition-transform duration-300',
      isOpen ? 'translate-x-0 animate__animated animate__slideInRight' : 'translate-x-full',
    ]"
  >
    <!-- Header del Sidebar -->
    <div class="flex items-center justify-between border-b border-gray-700 px-4 py-3">
      <h2 class="text-lg font-semibold text-white">Panel</h2>
      <button
        @click="closeSidebar"
        class="rounded-lg p-2 text-gray-400 transition-colors hover:bg-gray-700 hover:text-white"
      >
        <X class="h-5 w-5" />
      </button>
    </div>

    <!-- Contenido del Sidebar -->
    <div class="flex-1 overflow-y-auto p-4">
      <!-- Menú de navegación -->
      <div class="mb-6">
        <h3 class="mb-3 text-sm font-semibold uppercase tracking-wider text-gray-400">
          Navegación
        </h3>
        <div class="space-y-2">
          <button
            v-for="item in menuItems"
            :key="item.id"
            class="flex w-full items-center rounded-lg px-3 py-2 text-left text-sm text-gray-300 transition-colors hover:bg-gray-700 hover:text-white"
          >
            <component :is="item.icon" class="mr-3 h-4 w-4" />
            {{ item.name }}
          </button>
        </div>
      </div>

      <!-- Configuraciones -->
      <div class="mb-6">
        <h3 class="mb-3 text-sm font-semibold uppercase tracking-wider text-gray-400">
          Configuración
        </h3>
        <div class="space-y-3">
          <div class="flex items-center justify-between">
            <span class="text-sm text-gray-300">Modo oscuro</span>
            <button
              @click="toggleDarkMode"
              :class="[
                'relative inline-flex h-6 w-11 items-center rounded-full transition-colors',
                darkMode ? 'bg-teal-600' : 'bg-gray-600',
              ]"
            >
              <span
                :class="[
                  'inline-block h-4 w-4 transform rounded-full bg-white transition-transform',
                  darkMode ? 'translate-x-6' : 'translate-x-1',
                ]"
              />
            </button>
          </div>
        </div>
      </div>

      <!-- Información del usuario -->
      <div class="rounded-lg bg-gray-700 p-4">
        <div class="flex items-center">
          <div class="h-10 w-10 rounded-full bg-teal-600 flex items-center justify-center">
            <User class="h-5 w-5 text-white" />
          </div>
          <div class="ml-3">
            <h4 class="text-sm font-medium text-white">Jamel</h4>
            <p class="text-xs text-gray-400">Usuario administrador</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { X, User, Home, BarChart3, Settings, HelpCircle } from 'lucide-vue-next'

// Props
defineProps({
  isOpen: {
    type: Boolean,
    default: false,
  },
})

// Emits
const emit = defineEmits(['close'])

// Estado local
const darkMode = ref(true)

// Datos del menú
const menuItems = [
  { id: 'home', name: 'Inicio', icon: Home },
  { id: 'analytics', name: 'Análisis', icon: BarChart3 },
  { id: 'settings', name: 'Configuración', icon: Settings },
  { id: 'help', name: 'Ayuda', icon: HelpCircle },
]

// Funciones
const closeSidebar = () => {
  emit('close')
}

const toggleDarkMode = () => {
  darkMode.value = !darkMode.value
  console.log('Modo oscuro:', darkMode.value)
}
</script>

<style scoped>
/* Estilos adicionales para animaciones suaves */
.transition-transform {
  transition-property: transform;
  transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
}

/* Mejorar el scroll en el sidebar */
.overflow-y-auto::-webkit-scrollbar {
  width: 4px;
}

.overflow-y-auto::-webkit-scrollbar-track {
  background: transparent;
}

.overflow-y-auto::-webkit-scrollbar-thumb {
  background: rgba(156, 163, 175, 0.5);
  border-radius: 2px;
}

.overflow-y-auto::-webkit-scrollbar-thumb:hover {
  background: rgba(156, 163, 175, 0.7);
}
</style>
