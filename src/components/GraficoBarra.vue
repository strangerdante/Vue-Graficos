<template>
  <div class="h-auto w-full rounded-lg p-4">
    <div class="mb-4 flex items-center justify-between">
      <div>
        <h2 class="text-2xl font-bold text-white">Sales Comparison</h2>
        <p class="text-emerald-100">Than last day</p>
      </div>
      <div class="text-5xl font-bold text-white">94%</div>
    </div>
    <div class="h-[200px] w-auto">
      <canvas ref="chartCanvas"></canvas>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from "vue";
import Chart from "chart.js/auto";

export default {
  name: "SalesComparisonChart",
  setup() {
    const chartCanvas = ref(null);

    onMounted(() => {
      const ctx = chartCanvas.value.getContext("2d");
      new Chart(ctx, {
        type: "bar",
        data: {
          labels: ["06", "07", "08", "09", "10", "11", "12", "13", "14", "15"],
          datasets: [
            {
              data: [30, 70, 30, 40, 90, 60, 30, 70, 50, 90],
              backgroundColor: "white",
              barThickness: 8,
            },
            {
              data: [20, 40, 20, 30, 70, 50, 20, 50, 30, 80],
              backgroundColor: "rgba(255, 255, 255, 0.5)",
              barThickness: 8,
            },
          ],
        },
        options: {
          responsive: true,
          scales: {
            x: {
              grid: {
                display: false,
              },
              ticks: {
                color: "white",
              },
            },
            y: {
              display: false,
            },
          },
          plugins: {
            legend: {
              display: false,
            },
            datalabels: {
              display: false,
            },
          },
          barPercentage: 0.8,
          categoryPercentage: 0.9,
        },
      });
    });

    return {
      chartCanvas,
    };
  },
};
</script>
