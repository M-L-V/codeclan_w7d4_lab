<template>
    <div>
        <ul>
            <fuel-item v-for="(fuel, index) in childEnergyMix" :fuel="fuel" :key="index"></fuel-item>
        </ul>
    </div>
</template>

<script>
import FuelItem from './FuelItem';

export default {
    name: "list-item",
    props: ['childEnergyMix'],
    components: {
        "fuel-item": FuelItem
    }
}
</script>

<style lang="css">
    
</style>