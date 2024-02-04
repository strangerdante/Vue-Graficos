<template>
  <Line :data="data" :options="options" />
</template>

<script lang="ts">
import {
  Chart as ChartJS,
  CategoryScale,
  LinearScale,
  PointElement,
  LineElement,
  Title,
  Tooltip,
  Legend,
} from "chart.js";
import { Line } from "vue-chartjs";

ChartJS.register(
  CategoryScale,
  LinearScale,
  PointElement,
  LineElement,
  Title,
  Tooltip,
  Legend
);

export default {
  name: "GraficoLinea",
  components: {
    Line,
  },
  data() {
    return {
      data: {
        labels: ["Lunes", "Martes", "Miercoles", "Jueves", "Viernes"],
        datasets: [
          {
            label: "A",
            borderColor: "#13b497", // Color personalizado para las líneas
            data: [10, 30, 40, 20, 39, 80, 40],
            cubicInterpolationMode: "monotone", // Hace que las líneas sean curvas
          },
        ],
      },
      options: {
        responsive: true,
        maintainAspectRatio: false,
        plugins: {
          legend: {
            labels: {
              usePointStyle: true,
              pointStyle: "rect",
              color: "white",
            },
          },
        },
      },
    };
  },
};
</script>
