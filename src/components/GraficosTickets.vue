<template>
  <div class="flex w-full flex-col">
    <div class="mb-2 p-4">
      <h2 class="text-lg font-bold text-white">Mejores ventas</h2>
      <select
        v-model="selectedDay"
        class="mt-2 w-full rounded-xl bg-gray-800 p-4 text-sm text-white"
      >
        <option v-for="day in weekDays" :key="day" :value="day">
          {{ day }} - {{ dailySales[day].total }} pcs
        </option>
      </select>
    </div>

    <div
      class="flex flex-grow flex-col items-center justify-around gap-4 p-4 sm:flex-row"
    >
      <div class="relative aspect-square h-[200px] w-auto">
        <canvas ref="donutChart"></canvas>
      </div>
      <div class="relative h-[200px] w-auto">
        <canvas ref="barChart"></canvas>
      </div>
    </div>

    <div class="mt-2 flex justify-center gap-2 p-4">
      <div
        v-for="(color, ticket) in ticketColors"
        :key="ticket"
        class="flex items-center"
      >
        <div :class="`mr-1 h-3 w-3 rounded-full ${color}`"></div>
        <span class="text-xs text-white">{{ ticket }}</span>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted, watch } from "vue";
import Chart from "chart.js/auto";
import ChartDataLabels from "chartjs-plugin-datalabels";

Chart.register(ChartDataLabels);

export default {
  setup() {
    const selectedDay = ref("Martes");
    const donutChart = ref(null);
    const barChart = ref(null);
    let donutChartInstance = null;

    const weekDays = [
      "Domingo",
      "Lunes",
      "Martes",
      "Miercoles",
      "Jueves",
      "Viernes",
      "Sabado",
    ];
    const dailySales = {
      Domingo: { total: 180000, Peliculas: 20, Musica: 65, Futbol: 15 },
      Lunes: { total: 195000, Peliculas: 50, Musica: 35, Futbol: 15 },
      Martes: { total: 215523, Peliculas: 55, Musica: 35, Futbol: 10 },
      Miercoles: { total: 210000, Peliculas: 45, Musica: 40, Futbol: 15 },
      Jueves: { total: 200000, Peliculas: 12, Musica: 33, Futbol: 55 },
      Viernes: { total: 220000, Peliculas: 58, Musica: 30, Futbol: 12 },
      Sabado: { total: 190000, Peliculas: 48, Musica: 37, Futbol: 15 },
    };

    const ticketColors = {
      Peliculas: "bg-teal-300",
      Musica: "bg-teal-500",
      Futbol: "bg-teal-700",
    };

    const calculateTicketSales = (day) => {
      const { total, Peliculas, Musica, Futbol } = dailySales[day];
      return {
        Peliculas: Math.round((total * Peliculas) / 100),
        Musica: Math.round((total * Musica) / 100),
        Futbol: Math.round((total * Futbol) / 100),
      };
    };

    const createDonutChart = () => {
      const ctx = donutChart.value.getContext("2d");
      const salesData = calculateTicketSales(selectedDay.value);
      donutChartInstance = new Chart(ctx, {
        type: "doughnut",
        data: {
          labels: ["Peliculas", "Musica", "Futbol"],
          datasets: [
            {
              data: [salesData.Peliculas, salesData.Musica, salesData.Futbol],
              backgroundColor: ["#4fd1c5", "#319795", "#2c7a7b"],
            },
          ],
        },
        options: {
          responsive: true,
          plugins: {
            legend: {
              display: false,
            },
            tooltip: {
              enabled: false,
            },
            datalabels: {
              color: "#fff",
              formatter: (value, ctx) => {
                let sum = 0;
                let dataArr = ctx.chart.data.datasets[0].data;
                dataArr.map((data) => {
                  sum += data;
                });
                let percentage = ((value * 100) / sum).toFixed(0) + "%";
                return percentage;
              },
              font: {
                weight: "bold",
                size: 14,
              },
              anchor: "end",
              align: "start",
              offset: 15,
            },
          },
          cutout: "45%",
        },
      });
    };

    const updateDonutChart = () => {
      const salesData = calculateTicketSales(selectedDay.value);
      donutChartInstance.data.datasets[0].data = [
        salesData.Peliculas,
        salesData.Musica,
        salesData.Futbol,
      ];
      donutChartInstance.update();
    };

    const createBarChart = () => {
      const ctx = barChart.value.getContext("2d");
      new Chart(ctx, {
        type: "bar",
        data: {
          labels: weekDays,
          datasets: [
            {
              data: Object.values(dailySales).map((day) => day.total),
              backgroundColor: "#4fd1c5",
            },
          ],
        },
        options: {
          responsive: true,
          maintainAspectRatio: false,
          scales: {
            y: {
              beginAtZero: true,
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
        },
      });
    };

    onMounted(() => {
      createDonutChart();
      createBarChart();
    });

    watch(selectedDay, () => {
      updateDonutChart();
    });

    return {
      selectedDay,
      donutChart,
      barChart,
      weekDays,
      dailySales,
      ticketColors,
    };
  },
};
</script>
