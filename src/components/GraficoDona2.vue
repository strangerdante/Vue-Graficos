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
  name: "App",
  components: {
    Doughnut,
  },
  data() {
    return {
      data: {
        labels: ["Movies", "Music", "Footbal"],
        datasets: [
          {
            data: [35, 10, 55],
            backgroundColor: ["#13b497", "#0b6050", "#87ffe9"],
            hoverBackgroundColor: ["#FF6384", "#36A2EB", "#FFCE56"],
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
              pointStyle: "circle",
              color: "white",
            },
          },
        },
      },
    };
  },
};
</script>
