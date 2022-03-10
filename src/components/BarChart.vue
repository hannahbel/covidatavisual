<script>
import { Bar } from 'vue-chartjs'

export default {
  extends: Bar,
  props: {
        label: {
            type: String
        },
        chartData: {
            type: Array
        },
        options: {
            type: Object
        },
       
    },
    mounted() {
        this.renderChart({
            labels: ['January', 'February', 'March', 'April', 'May'],
            datasets: [
                {
                    label: this.label,
                    data: [27318, 29763, 130245, 73908, 54290],
                    backgroundColor: '#f87979',
                }
            ],
  });
},
}

</script>
