<template>
  <div class="w-1/2">
    <canvas class="p-10" ref="zipChart"></canvas>
  </div>
</template>

<!-- changed script section to switch from Options to Composition API -->
<script>
import { Chart, registerables } from 'chart.js'
import { ref, onMounted } from 'vue'

export default {
  props: {
    label: {
      type: Array,
      required: true,
    },
    chartData: {
      type: Array,
      required: true,
    }
  },
  setup(props) {
    const zipChart = ref(null);

    onMounted(() => {
      Chart.register(...registerables);

      // Initialize the chart
      const ctx = zipChart.value.getContext('2d');
      new Chart(ctx, {
        type: 'doughnut',
        data: {
          labels: props.label,
          datasets: [
            {
              borderWidth: 1,
              data: props.chartData,
              backgroundColor: [
                'rgba(255, 99, 132, 0.2)',
                'rgba(54, 162, 235, 0.2)',
                'rgba(255, 206, 86, 0.2)',
                'rgba(75, 192, 192, 0.2)',
                'rgba(153, 102, 255, 0.2)',
                'rgba(255, 159, 64, 0.2)'
              ],
              borderColor: [
                'rgba(255, 99, 132, 1)',
                'rgba(54, 162, 235, 1)',
                'rgba(255, 206, 86, 1)',
                'rgba(75, 192, 192, 1)',
                'rgba(153, 102, 255, 1)',
                'rgba(255, 159, 64, 1)'
              ],
              borderWidth: 1
            }
          ]
        },
        options: {
          plugins: {
            legend: {
              display: true
            },
            title: {
              display: true,
              text: 'Clients by Zip Code'
            }
          },
          responsive: true,
          maintainAspectRatio: true
        }
      });
    });

    return {
      zipChart
    };
  }
}
</script>

<!--Original Options API code for reference:
<script>
import { Chart, registerables } from 'chart.js'
Chart.register(...registerables)
//define props (label and chartData)
export default {
  props: {
    label: {
      type: Array
    },
    chartData: {
      type: Array
    }
  },
  async mounted() { //uses the data to load the chart's values
    await new Chart(this.$refs.zipChart, {
      type: 'doughnut',
      data: {
        labels: this.label,
        datasets: [
          {
            borderWidth: 1,
            data: this.chartData // Update this line
          }
        ]
      },
      options: {
        plugins: {
          legend: {
            display: false
          },
          title: {
            display: true,
            text: 'Clients by Zip Code'
          }
        },
        responsive: true,
        maintainAspectRatio: true
      }
    })
  },
}
</script> -->

