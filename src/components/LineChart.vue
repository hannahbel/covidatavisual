<script>
import {Line} from "vue-chartjs";

export default {
    extends: Line,
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
        chartColors: {
            Type: Object
        }
    },
    mounted() {
        const dates = this.chartData.map(d => d.lastUpdatedAtApify);
        const infec = this.chartData.map(d => d.infected);
        const recov = this.chartData.map(d => d.recovered);
        const decea = this.chartData.map(d => d.deceased);

        const {borderColor, pointBorderColor, pointBackgroundColor, backgroundColor} = this.chartColors;
        this.renderChart({
            labels: dates,
            datasets: [
                {
                label: this.label,
                data: infec, 
                borderColor: borderColor,
                pointBorderColor: pointBorderColor,
                pointBackgroundColor: pointBackgroundColor,
                backgroundColor: backgroundColor
            },
              {
                label: this.label,
                data: recov, 
                borderColor: borderColor,
                pointBorderColor: pointBorderColor,
                pointBackgroundColor: pointBackgroundColor,
                backgroundColor: backgroundColor
            },
            {
                label: this.label,
                data: decea, 
                borderColor: borderColor,
                pointBorderColor: pointBorderColor,
                pointBackgroundColor: pointBackgroundColor,
                backgroundColor: backgroundColor
            }
            ],
        },
        this.options
        );
    },
}
</script>
