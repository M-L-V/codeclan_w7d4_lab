<template>
    <div>
        From: {{fromDate}} - To: {{toDate}}
        <ul>
            <fuel-item v-for="(fuel, index) in childEnergyMix" :fuel="fuel" :key="index"></fuel-item>
        </ul>
    </div>
</template>

<script>
import FuelItem from './FuelItem';

export default {
    name: "list-item",
    props: ['childEnergyMix', 'fromDate', 'toDate'],
    components: {
        "fuel-item": FuelItem   
    }
}
</script>

<style lang="css">
    
</style>