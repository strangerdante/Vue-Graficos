<template>
  <!-- Barra superior -->
  <div
    class="relative flex items-center justify-between bg-gray-800 px-4 py-3 shadow-sm sm:px-6"
  >
    <!-- Lado izquierdo: Título -->
    <div class="flex items-center">
      <h1 class="text-lg font-semibold text-white">Dashboard</h1>
    </div>

    <!-- Lado derecho: Iconos y usuario -->
    <div class="flex items-center space-x-4">
      <!-- Botón de alertas -->
      <div class="relative" data-dropdown="notifications">
        <button
          class="relative rounded-lg p-2 text-gray-400 transition-colors hover:bg-gray-700 hover:text-white focus:outline-none focus:ring-2 focus:ring-teal-500"
          @click="toggleNotifications"
        >
          <Bell class="h-5 w-5" />
          <!-- Indicador de notificaciones -->
          <span
            v-if="unreadNotifications > 0"
            class="absolute -right-1 -top-1 flex h-4 w-4 items-center justify-center rounded-full bg-teal-500 text-xs text-white"
          >
            {{ unreadNotifications > 9 ? "9+" : unreadNotifications }}
          </span>
        </button>

        <!-- Dropdown de notificaciones -->
        <div
          v-if="showNotifications"
          class="absolute left-1/2 top-full z-50 mt-2 w-72 -translate-x-1/2 rounded-lg bg-white shadow-lg ring-1 ring-black ring-opacity-5 sm:left-auto sm:right-0 sm:w-80 sm:translate-x-0"
        >
          <div class="p-4">
            <div class="flex items-center justify-between border-b pb-2">
              <h3 class="text-sm font-semibold text-gray-900">
                Notificaciones
              </h3>
              <button
                @click="markAllAsRead"
                class="text-xs text-teal-600 hover:text-teal-800"
              >
                Marcar todas como leídas
              </button>
            </div>
            <div class="mt-3 max-h-64 overflow-y-auto">
              <div
                v-for="notification in notifications"
                :key="notification.id"
                class="flex cursor-pointer items-start space-x-3 rounded py-2 hover:bg-gray-50"
                @click="markAsRead(notification.id)"
              >
                <div class="flex-shrink-0">
                  <div
                    class="h-2 w-2 rounded-full bg-teal-500"
                    v-if="!notification.read"
                  ></div>
                  <div class="h-2 w-2" v-else></div>
                </div>
                <div class="min-w-0 flex-1">
                  <p class="text-sm font-medium text-gray-900">
                    {{ notification.title }}
                  </p>
                  <p class="mt-1 text-xs text-gray-500">
                    {{ notification.message }}
                  </p>
                  <p class="mt-1 text-xs text-gray-400">
                    {{ notification.time }}
                  </p>
                </div>
              </div>
              <div
                v-if="notifications.length === 0"
                class="py-4 text-center text-sm text-gray-500"
              >
                No hay notificaciones
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Botón de mensajes -->
      <div class="relative" data-dropdown="messages">
        <button
          class="relative rounded-lg p-2 text-gray-400 transition-colors hover:bg-gray-700 hover:text-white focus:outline-none focus:ring-2 focus:ring-blue-500"
          @click="toggleMessages"
        >
          <Mail class="h-5 w-5" />
          <!-- Indicador de mensajes -->
          <span
            v-if="unreadMessages > 0"
            class="absolute -right-1 -top-1 flex h-4 w-4 items-center justify-center rounded-full bg-blue-500 text-xs text-white"
          >
            {{ unreadMessages > 9 ? "9+" : unreadMessages }}
          </span>
        </button>

        <!-- Dropdown de mensajes -->
        <div
          v-if="showMessages"
          class="absolute left-1/2 top-full z-50 mt-2 w-72 -translate-x-1/2 rounded-lg bg-white shadow-lg ring-1 ring-black ring-opacity-5 sm:left-auto sm:right-0 sm:w-80 sm:translate-x-0"
        >
          <div class="p-4">
            <div class="flex items-center justify-between border-b pb-2">
              <h3 class="text-sm font-semibold text-gray-900">Mensajes</h3>
              <button
                @click="goToMessages"
                class="text-xs text-blue-600 hover:text-blue-800"
              >
                Ver todos
              </button>
            </div>
            <div class="mt-3 max-h-64 overflow-y-auto">
              <div
                v-for="message in messages"
                :key="message.id"
                class="flex cursor-pointer items-start space-x-3 rounded border-b py-3 last:border-b-0 hover:bg-gray-50"
                @click="openMessage(message.id)"
              >
                <div
                  class="flex h-8 w-8 items-center justify-center rounded-full bg-gray-600"
                >
                  <span class="text-xs font-medium text-white">
                    {{ message.sender.charAt(0).toUpperCase() }}
                  </span>
                </div>
                <div class="min-w-0 flex-1">
                  <div class="flex items-center justify-between">
                    <p class="text-sm font-medium text-gray-900">
                      {{ message.sender }}
                    </p>
                    <p class="text-xs text-gray-500">{{ message.time }}</p>
                  </div>
                  <p class="mt-1 truncate text-sm text-gray-600">
                    {{ message.preview }}
                  </p>
                </div>
                <div class="flex-shrink-0">
                  <div
                    class="h-2 w-2 rounded-full bg-blue-500"
                    v-if="!message.read"
                  ></div>
                </div>
              </div>
              <div
                v-if="messages.length === 0"
                class="py-4 text-center text-sm text-gray-500"
              >
                No hay mensajes
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Botón de regalos/paquetes -->
      <button
        class="rounded-lg p-2 text-gray-400 transition-colors hover:bg-gray-700 hover:text-white focus:outline-none focus:ring-2 focus:ring-gray-500"
        @click="toggleGifts"
      >
        <Gift class="h-5 w-5" />
      </button>

      <!-- Avatar y menú de usuario -->
      <div class="relative" data-dropdown="user">
        <button
          class="flex items-center space-x-2 rounded-lg p-1 transition-colors hover:bg-gray-700 focus:outline-none focus:ring-2 focus:ring-gray-500 sm:space-x-3"
          @click="toggleUserMenu"
        >
          <div
            class="flex h-8 w-8 items-center justify-center rounded-full bg-gray-600"
          >
            <span class="text-sm font-medium text-white">J</span>
          </div>
          <span class="hidden text-sm font-medium text-white sm:block"
            >Jamel</span
          >
          <ChevronDown class="h-3 w-3 text-gray-400" />
        </button>

        <!-- Dropdown del usuario -->
        <div
          v-if="showUserMenu"
          class="absolute right-0 top-full z-50 mt-2 w-48 rounded-lg bg-white shadow-lg ring-1 ring-black ring-opacity-5"
        >
          <div class="py-1">
            <div class="border-b px-4 py-3">
              <p class="text-sm font-medium text-gray-900">Jamel</p>
              <p class="text-xs text-gray-500">jamel@example.com</p>
            </div>
            <button
              @click="goToProfile"
              class="flex w-full items-center px-4 py-2 text-sm text-gray-700 hover:bg-gray-100"
            >
              <User class="mr-3 h-4 w-4" />
              Mi Perfil
            </button>
            <div class="border-t">
              <button
                @click="logout"
                class="flex w-full items-center px-4 py-2 text-sm text-red-600 hover:bg-red-50"
              >
                <LogOut class="mr-3 h-4 w-4" />
                Cerrar Sesión
              </button>
            </div>
          </div>
        </div>
      </div>

      <!-- Botón del sidebar -->
      <button
        class="rounded-lg p-2 text-gray-400 transition-colors hover:bg-gray-700 hover:text-white focus:outline-none focus:ring-2 focus:ring-gray-500"
        @click="toggleSidebar"
      >
        <Menu class="h-5 w-5" />
      </button>
    </div>
  </div>

  <!-- Overlay para cerrar dropdowns -->
  <div
    v-if="showNotifications || showMessages || showUserMenu"
    class="fixed inset-0 z-40 bg-black bg-opacity-25 lg:bg-transparent"
    @click="closeAllDropdowns"
  ></div>
</template>

<script setup>
import {
  Bell,
  Mail,
  Gift,
  Menu,
  ChevronDown,
  User,
  LogOut,
} from "lucide-vue-next";
import { ref, computed, onMounted, onUnmounted } from "vue";

// Emits
const emit = defineEmits(["toggle-sidebar"]);

// Estado reactivo para los dropdowns
const showNotifications = ref(false);
const showMessages = ref(false);
const showUserMenu = ref(false);

// Datos de ejemplo para notificaciones
const notifications = ref([
  {
    id: 1,
    title: "Nueva actualización disponible",
    message: "Se ha lanzado una nueva versión del sistema",
    time: "hace 5 min",
    read: false,
  },
  {
    id: 2,
    title: "Recordatorio de reunión",
    message: "Reunión de equipo en 30 minutos",
    time: "hace 25 min",
    read: false,
  },
  {
    id: 3,
    title: "Tarea completada",
    message: "El informe mensual ha sido generado",
    time: "hace 2 horas",
    read: true,
  },
]);

// Datos de ejemplo para mensajes
const messages = ref([
  {
    id: 1,
    sender: "María García",
    preview: "¿Podemos revisar el proyecto mañana?",
    time: "hace 10 min",
    read: false,
  },
  {
    id: 2,
    sender: "Carlos López",
    preview: "Los datos del dashboard están listos",
    time: "hace 1 hora",
    read: false,
  },
  {
    id: 3,
    sender: "Ana Martínez",
    preview: "Excelente trabajo en la presentación",
    time: "hace 3 horas",
    read: true,
  },
]);

// Computed properties para contadores
const unreadNotifications = computed(() => {
  return notifications.value.filter((n) => !n.read).length;
});

const unreadMessages = computed(() => {
  return messages.value.filter((m) => !m.read).length;
});

// Funciones para los dropdowns
const toggleNotifications = () => {
  showNotifications.value = !showNotifications.value;
  showMessages.value = false;
  showUserMenu.value = false;
};

const toggleMessages = () => {
  showMessages.value = !showMessages.value;
  showNotifications.value = false;
  showUserMenu.value = false;
};

const toggleUserMenu = () => {
  showUserMenu.value = !showUserMenu.value;
  showNotifications.value = false;
  showMessages.value = false;
};

const closeAllDropdowns = () => {
  showNotifications.value = false;
  showMessages.value = false;
  showUserMenu.value = false;
};

// Funciones para notificaciones
const markAsRead = (id) => {
  const notification = notifications.value.find((n) => n.id === id);
  if (notification) {
    notification.read = true;
  }
};

const markAllAsRead = () => {
  notifications.value.forEach((n) => (n.read = true));
};

// Funciones para mensajes
const openMessage = (id) => {
  const message = messages.value.find((m) => m.id === id);
  if (message) {
    message.read = true;
  }
  console.log("Abriendo mensaje:", id);
  // Aquí puedes agregar navegación a la vista de mensajes
};

const goToMessages = () => {
  console.log("Navegando a todos los mensajes");
  closeAllDropdowns();
  // Aquí puedes agregar navegación a la vista de mensajes
};

// Funciones del menú de usuario
const goToProfile = () => {
  console.log("Navegando al perfil");
  closeAllDropdowns();
  // Aquí puedes agregar navegación al perfil
};

const goToSettings = () => {
  console.log("Navegando a configuración");
  closeAllDropdowns();
  // Aquí puedes agregar navegación a configuración
};

const goToHelp = () => {
  console.log("Navegando a ayuda");
  closeAllDropdowns();
  // Aquí puedes agregar navegación a ayuda
};

const logout = () => {
  console.log("Cerrando sesión");
  closeAllDropdowns();
  // Aquí puedes agregar la lógica de cierre de sesión
};

const toggleGifts = () => {
  console.log("Abriendo regalos/paquetes");
  // Aquí puedes agregar la lógica para mostrar/ocultar regalos
};

const toggleSidebar = () => {
  emit("toggle-sidebar");
};

// Cerrar dropdowns al hacer clic fuera
const handleClickOutside = (event) => {
  // Verificar si el clic fue fuera de los dropdowns específicos
  const notificationDropdown = event.target.closest(
    '[data-dropdown="notifications"]'
  );
  const messageDropdown = event.target.closest('[data-dropdown="messages"]');
  const userDropdown = event.target.closest('[data-dropdown="user"]');

  if (!notificationDropdown && !messageDropdown && !userDropdown) {
    closeAllDropdowns();
  }
};

onMounted(() => {
  document.addEventListener("click", handleClickOutside);
});

onUnmounted(() => {
  document.removeEventListener("click", handleClickOutside);
});
</script>

<style scoped>
/* Estilos para el navbar */
</style>
