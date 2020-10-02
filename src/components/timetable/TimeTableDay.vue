<template>
    <div>
        <select v-on:change="whichDay($event)">
            <option :value="today">Today</option>
            <option :value="tomorrow">Tomorrow</option>
        </select>
    </div>
</template>

<script>
export default {
    name: "TimeTableDay",
    data() {
        return {
            today: this.getToday(),
            tomorrow: this.getTomorrow()
        }
    },
    methods: {
        getToday() {
            var today = new Date();
            var dd = String(today.getDate()).padStart(2, '0');
            var mm = String(today.getMonth() + 1).padStart(2, '0'); //January is 0!
            var yyyy = today.getFullYear();

            today = dd + '/' + mm + '/' + yyyy;
            return today;
        },
        getTomorrow() {
            var tomorrow = new Date();
            var dd = String(tomorrow.getDate() + 1).padStart(2, '0');
            var mm = String(tomorrow.getMonth() + 1).padStart(2, '0'); //January is 0!
            var yyyy = tomorrow.getFullYear();

            tomorrow = dd + '/' + mm + '/' + yyyy;
            return tomorrow;
        },
        whichDay(event) {
            this.$emit('date', event.target.value)
        }
    }    
}
</script>

<style scoped>

</style>