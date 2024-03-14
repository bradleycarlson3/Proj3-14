<template>
  <div>
    <canvas class="p-10" ref="attendanceChart"></canvas>
  </div>
</template>
<!-- modified script section to switch from Options to Composition API -->

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
    const attendanceChart = ref(null);

    onMounted(() => {
      Chart.register(...registerables);

      // Initialize the chart
      const ctx = attendanceChart.value.getContext('2d');
      new Chart(ctx, {
        type: 'bar',
        data: {
          labels: props.label,
          datasets: [
            {
              label: 'Attendance',
              borderWidth: 1,
              data: props.chartData,
              backgroundColor: 'rgba(54, 162, 235, 0.2)',
              borderColor: 'rgba(54, 162, 235, 1)',
              borderWidth: 1
            }
          ]
        },
        options: {
          scales: {
            y: {
              beginAtZero: true,
              ticks: {
                stepSize: 1
              }
            }
          },
          plugins: {
            legend: {
              display: false
            },
            title: {
              display: true,
              text: 'Attendance Chart'
            }
          },
          responsive: true,
          maintainAspectRatio: true
        }
      });
    });

    return {
      attendanceChart
    };
  }
}
</script>


<!-- The original Options API script section (for reference):
<script>
import { Chart, registerables } from 'chart.js'
import { Colors } from 'chart.js';

Chart.register(...registerables)
Chart.register(Colors);

export default {
  props: {
    label: {
      type: Array
    },
    chartData: {
      type: Array
    }
  },
  async mounted() {
    await new Chart(this.$refs.attendanceChart, {
      type: 'bar',
      data: {
        labels: this.label,
        datasets: [
          {
            borderWidth: 1,
            data: this.chartData
          }
        ]
      },
      options: {
        scales: {
          y: {
            ticks: {
              stepSize: 1
            }
          },
          x: {
            gridLines: {
              display: false
            }
          }
        },
        plugins: {
          legend: {
            display: false
          },
          title: {
            display: true,
            text: 'Attendance Chart'
          }
        },
        responsive: true,
        maintainAspectRatio: true
      }
    })
  }
}
</script> -->

