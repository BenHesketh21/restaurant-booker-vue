<template>
    <div id="Bookings">
        <BookingAvailable v-on:booking-avail="isAvailable" v-bind:booking="booking" />
    </div>
</template>

<script>
import BookingAvailable from '../components/bookings/BookingAvailable';
import axios from 'axios';

export default {
    name: "Bookings",
    components: {
        BookingAvailable
    },
    data() {
        return {
            booking: {
                available: null,
                message: '',
                table:''
            },
            retry: false
        }
    },
    methods: {
        isAvailable(requestedBooking) {
            console.log(requestedBooking)
            axios.post('http://localhost:5000/bookings/available', requestedBooking).then( res =>{
            this.booking.available = res.data.available
            this.booking.message = res.data.message
            this.booking.table = Number(res.data.table)
            });
        //    console.log(requestedBooking)
          //  if (this.retry == true) {
        //    this.booking.available = false
        //    this.booking.message = "Not available"
        //    this.booking.table = ""
        //    this.retry = false
        //    }
        //    else {
        //    this.booking.available = true
         //   this.booking.message = "Available"
        //    this.booking.table = 5
        //    this.retry = true  
        //    }
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