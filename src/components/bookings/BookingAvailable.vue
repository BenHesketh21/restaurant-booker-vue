<template>
    <div>
        When would you like to book?
        <br>
        <br>
        <form @submit.prevent="isAvailable">
        <input type="date" v-model="date" name="" id="">
        <br><br>
        <input type="time" v-model="time" name="" id="">
        <br><br>
        <input type="number" v-model="num_of_cust" name="" id="">
        <br><br>
        <input type="submit" value="Check Availability">
        </form>
        <br><br>
        <div v-if="booking.available">
            {{ booking.message }}
            <br><br>
            Table Available: {{ booking.table }}            
            Book?
            <br><br>
            <button>&#10004;</button>
            <button>X</button>
        </div>
        <div v-else>
            {{ booking.message }}
        </div>
    </div>
</template>

<script>
export default {
    name: "BookingAvailable",
    props: ['booking'],
    methods: {
        isAvailable() {
            const requestedBooking = {
                date: this.date,
                time: this.time,
                num_of_cust: this.num_of_cust
            }
            this.$emit('booking-avail', requestedBooking)
        }
    }
}
</script>

<style scoped>

</style>