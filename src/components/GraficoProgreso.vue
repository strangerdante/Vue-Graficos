<template>
  <div class="flex-col p-6">
    <div class="flex-col">
      <div class="flex">
        <p class="font-bold text-white">{{ currentValue }} Pcs</p>
        <div class="ml-auto flex items-center">
          <select
            v-model="selectedPeriod"
            class="mr-2 appearance-none rounded-xl bg-gray-800 py-2 pl-2 pr-8 text-sm text-white"
            style="
              background-image: url('data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTQiIGhlaWdodD0iOCIgdmlld0JveD0iMCAwIDE0IDgiIGZpbGw9Im5vbmUiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyI+CjxwYXRoIGQ9Ik0xIDFMNyA3TDEzIDEiIHN0cm9rZT0iI2ZmZmZmZiIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbGluZWNhcD0icm91bmQiIHN0cm9rZS1saW5lam9pbj0icm91bmQiLz4KPC9zdmc+');
              background-repeat: no-repeat;
              background-position: right 0.5rem center;
              background-size: 10px 8px;
            "
          >
            <option value="daily" class="bg-gray-800 text-white">Diario</option>
            <option value="weekly" class="bg-gray-800 text-white">
              Semanal
            </option>
            <option value="monthly" class="bg-gray-800 text-white">
              Mensual
            </option>
          </select>
        </div>
      </div>
      <p class="text-gray-500">Tickets Vendido</p>
    </div>
    <div class="mt-3 h-2.5 w-full rounded-full bg-gray-200 dark:bg-gray-500">
      <div
        class="h-2.5 rounded-full bg-verde transition-all duration-500 ease-in-out"
        :style="{ width: `${currentPercentage}%` }"
      ></div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      selectedPeriod: "daily",
      values: {
        daily: 456000,
        weekly: 3192000,
        monthly: 13680000,
      },
      percentages: {
        daily: 70,
        weekly: 80,
        monthly: 90,
      },
    };
  },
  computed: {
    currentValue() {
      const value = this.values[this.selectedPeriod];
      return value >= 1000000
        ? `${(value / 1000000).toFixed(2)}M`
        : `${(value / 1000).toFixed(0)}k`;
    },
    currentPercentage() {
      return this.percentages[this.selectedPeriod];
    },
  },
};
</script>

<style scoped>
/* Estilos adicionales si son necesarios */
</style>
