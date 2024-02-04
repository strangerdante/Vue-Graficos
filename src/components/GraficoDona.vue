<template>
  <Doughnut :data="data" :options="options" />
</template>
<script lang="ts">
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  ArcElement,
  CategoryScale,
} from "chart.js";
import { Doughnut } from "vue-chartjs";

ChartJS.register(ArcElement, CategoryScale, Title, Tooltip, Legend);

export default {
  name: "GraficoDona",
  components: {
    Doughnut,
  },
  data() {
    return {
      data: {
        labels: ["A", "B", "C", "D"],
        datasets: [
          {
            data: [40, 30, 20, 10],
            backgroundColor: ["#FF6384", "#36A2EB", "#FFCE56", "#1bd344"],
            hoverBackgroundColor: ["#FF6384", "#36A2EB", "#FFCE56", "#1bd344"],
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
