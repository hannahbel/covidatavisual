<script>
import { Pie } from 'vue-chartjs'

export default {
  extends: Pie,
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
            labels: ['Positive', 'Recovered', 'Deceased', 'Active'],
            datasets: [
                {
                    backgroundColor: [ '#FF0000', '#1E9600', '#007580', '#F48B29'],
					data: [1327431, 1246405, 22963, 58063],
                }
            ],
  });
},
}

</script>
