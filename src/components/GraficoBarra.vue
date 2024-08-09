<template>
  <Bar :data="data" :options="options" />
</template>

<script lang="ts">
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  BarElement,
  CategoryScale,
  LinearScale,
} from "chart.js";
import { Bar } from "vue-chartjs";

ChartJS.register(
  CategoryScale,
  LinearScale,
  BarElement,
  Title,
  Tooltip,
  Legend
);

export default {
  name: "GraficoBarra",
  components: {
    Bar,
  },
  data() {
    return {
      data: {
        labels: ["L", "M", "M", "J", "V", "S", "D"],
        datasets: [
          {
            label: "Barras 1",
            data: [40, 20, 12, 10, 20, 40, 50],
            backgroundColor: ["#ffffff"],
          },
          {
            label: "Barras 2",
            data: [30, 10, 25, 15, 35, 20, 45],
            backgroundColor: ["#13b497"],
          },
        ],
      },
      options: {
        responsive: true,
        plugins: {
          legend: {
            position: "right",
            align: "center",
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
