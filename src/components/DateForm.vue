<template>
    <form>
        <input type='datetime-local' v-on:input="onDateInput">
        <input type='datetime-local' v-on:input="toDateInput">
    </form>
</template>

<script>
import { eventBus } from '../main';
export default {
    name: "date-form",
    methods: {
        onDateInput: function(e) {
            eventBus.$emit("input-from-date", e.target.value)
        },
        toDateInput: function(e){
            eventBus.$emit("input-to-date", e.target.value)
        }
    }

}
</script>

<style lang="css">
    
</style>