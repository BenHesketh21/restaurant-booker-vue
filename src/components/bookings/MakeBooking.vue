<template>
    <div id="makeBooking">                 
        <br>
        <h3>Table {{ table }} is available            
        Would you like to book it?</h3>
        <br><br>
        <button v-on:click="makeBooking">&#10004;</button>
        <button v-on:click="noBooking">X</button>
    </div>


</template>

<script>

export default {
    props: ['time', 'date', 'table'],
    methods: {
        makeBooking() {
            let formattedDate = this.date[8] + this.date[9] + '/' + this.date[5] + this.date[6] + '/' + this.date[0] + this.date[1] + this.date[2] + this.date[3]
            let approvedBooking = {
                date: formattedDate,
                time: this.time,
                user: 1,
                table: this.table
            }
            this.$emit('make-booking', approvedBooking)
        },
        noBooking() {
            this.$emit('no-booking')
        }
    }
}
</script>

<style scoped>

</style>