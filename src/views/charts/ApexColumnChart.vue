<script setup lang="ts">
import { computed } from 'vue';
import { useTheme } from 'vuetify';
import { getPrimary, getSecondary } from '@/utils/UpdateColors';
import { ref } from 'vue';
import UiParentCard from '@/components/shared/UiParentCard.vue';
import UiChildCard from '@/components/shared/UiChildCard.vue';
// common components
import BaseBreadcrumb from '@/components/shared/BaseBreadcrumb.vue';
// theme breadcrumb
const page = ref({ title: 'Column Chart' });
const breadcrumbs = ref([
    {
        text: 'Home',
        disabled: false,
        href: '#'
    },
    {
        text: 'Column chart',
        disabled: true,
        href: '#'
    }
]);

const theme = useTheme();
const chartOptions = computed(() => {
    return {
        chart: {
            type: 'bar',
            height: 350,
            fontFamily: `inherit`,
            toolbar: {
              show: false,
            },
        },
        colors: ['#6ac3fd', '#0b70fb', '#f64e60'],
        plotOptions: {
            bar: {
                horizontal: false,
                endingShape: 'rounded',
                columnWidth: '20%'
            }
        },
        dataLabels: {
            enabled: false,
        },
        stroke: {
            show: true,
            width: 2,
            colors: ['transparent']
        },

        xaxis: {
            categories: ['Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct'],
            labels: {
                style: {
                    colors: '#adb0bb'
                }
            }
        },
        yaxis: {
          title: {
            text: '$ (thousands)',
            
          },
          labels: {
                style: {
                    colors: '#adb0bb'
                }
            }
        },
        fill: {
            opacity: 1
        },
       
        tooltip: {
            theme: 'dark',
            y: {
              formatter(val:any) {
                return `$ ${val} thousands`;
              },
            },
        },
        grid: {
          show: false,
        },
        legend: {
          show: true,
          position: 'bottom',
          width: '50px',
          labels: {
          colors: 'adb0bb',

            },
        },
        responsive: [
            {
                breakpoint: 600,
                options: {
                    yaxis: {
                        show: false
                    }
                }
            }
        ]
    };
});

const columnChart = {
    series: [
        {
            name: 'Desktop',
            data: [44, 55, 57, 56, 61, 58, 63, 60, 66]
        },
        {
            name: 'Mobile',
            data: [76, 85, 101, 98, 87, 105, 91, 114, 94]
        },
        {
            name: 'Other',
            data: [35, 41, 36, 26, 45, 48, 52, 53, 41]
        }
    ]
};
</script>

<template>
    <!-- ---------------------------------------------------- -->
    <!-- Column Chart -->
    <!-- ---------------------------------------------------- -->
    <BaseBreadcrumb :title="page.title" :breadcrumbs="breadcrumbs"></BaseBreadcrumb>
    <v-row>
        <v-col cols="12">
            <UiParentCard title="Column Chart">
                <apexchart type="bar" height="300" :options="chartOptions" :series="columnChart.series"> </apexchart>
            </UiParentCard>
        </v-col>
    </v-row>
</template>
