<template>
    <div>
        <GChart
            type="PieChart"
            :data="childEnergyMix"
        />
    </div>
</template>

<script>
import { GChart } from 'vue-google-charts'
 
export default {
    name: 'fuel-chart',
    
       
        
    
    props: ['childEnergyMix'],
    components: {
        GChart
    }
}
</script>

<style lang="css">
    
</style>