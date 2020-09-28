<template>
    <div id="Bookings">
        <BookingAvailable v-on:booking-avail="isAvailable" v-bind:booking="booking" />
    </div>
</template>

<script>
import BookingAvailable from '../components/bookings/BookingAvailable';

export default {
    name: "Bookings",
    components: {
        BookingAvailable
    },
    data() {
        return {
            booking: {
                available: false,
                message: '',
                table:''
            }
        }
    },
    methods: {
        isAvailable(requestedBooking) {
            console.log(requestedBooking)
            this.booking.available = false
            this.booking.message = "NOT available"
            this.booking.table = null
          //  return {
          //      available: false,
          //      message: "Not available" 
          //  }
        }
    }
    
}
</script>

<style scoped>

</style>