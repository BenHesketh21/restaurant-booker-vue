<template>
    <div id="Bookings">
        <BookingAvailable v-on:make-booking="makeBooking" v-on:booking-avail="isAvailable" v-bind:booking="booking" />
    </div>
</template>

<script>
import BookingAvailable from '../components/bookings/BookingAvailable';
//import axios from 'axios';
import uuid from 'uuid';

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
            retry: false,
            bookings: [
                {
                    id: 1,
                    time:"13:00:00",
                    date:"28/09/2020",
                    table:1,
                    user:1,
                    arrived: false
                },
                {
                    id: 2,
                    time:"15:30:00",
                    date:"29/09/2020",
                    table:2,
                    user:1,
                    arrived: false
                },
                {
                    id: 3,
                    time:"14:30:00",
                    date:"28/09/2020",
                    table:3,
                    user:2,
                    arrived: false
                },
                {
                    id: 4,
                    time:"16:30:00",
                    date:"29/09/2020",
                    table:1,
                    user:2,
                    arrived: false
                },
                {
                    id: 5,
                    time:"12:30:00",
                    date:"28/09/2020",
                    table:3,
                    user:3,
                    arrived: false
                },
                {
                    id: 6,
                    time:"13:30:00",
                    date:"29/09/2020",
                    table:1,
                    user:1,
                    arrived: false
                },
                {
                    id: 7,
                    time:"18:30:00",
                    date:"28/09/2020",
                    table:2,
                    user:1,
                    arrived: false
                },
                {
                    id: 8,
                    time:"19:00:00",
                    date:"29/09/2020",
                    table:2,
                    user:2,
                    arrived: false
                },
                {
                    id: 9,
                    time:"12:00:00",
                    date:"28/09/2020",
                    table:4,
                    user:2,
                    arrived: false
                }       
            ]
        }
    },
    methods: {
        isAvailable(requestedBooking) {
            console.log(requestedBooking)
            // axios.post('http://localhost:5000/bookings/available', requestedBooking).then( res =>{
            this.booking.available = true
            this.booking.message = "yes this table is available"
            this.booking.table = 1
            //});
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
        },
        makeBooking(approvedBooking) {
            let newBooking = {
                id: uuid,
                table: approvedBooking.table,
                user: approvedBooking.user,
                time: approvedBooking.time,
                date: approvedBooking.date,
                arrived: false
            }
            this.bookings = [...this.bookings, newBooking]
        }
    }
    
}
</script>

<style scoped>

</style>