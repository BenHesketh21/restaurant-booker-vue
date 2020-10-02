<template>
    <div v-if="isThereBookings(time.time)">
        <p class="time-slot">{{ time.time }} </p>
        <table>
        <tr class="headings">
            <th id="cust_name">Customer Name</th>
            <th id="table_num">Table Number</th>
            <th id="blank"></th>
        </tr>
        </table>
        <p v-bind:key="booking.id" v-for="booking in isThereBookings(time.time)">
            <TimeTableBooking v-bind:booking="booking" v-bind:customer="getCustomer(booking.user)" v-bind:table="getTable(booking.id)" v-on:del-booking="delBooking" />
        </p>
    </div>
    <div v-else>
        <p class="time-slot">{{ time.time }}</p>
    </div>
</template>

<script>
import TimeTableBooking from './TimeTableBooking';


export default {
    name: "TimeTableSlot",
    props: ["time", "bookings", "customers", "tables", "date"],
    components: {
        TimeTableBooking
    },
    methods: {
        isThereBookings(time) {
        var booking;
        var bookingsList = []
        for (booking in this.bookings) {
            console.log(this.bookings[booking].time, time, this.bookings[booking].date, this.date)
            if (this.bookings[booking].time == time && this.bookings[booking].date == this.date) {
                bookingsList.push(this.bookings[booking])
            }           
        }
        if (bookingsList.length > 0) {
            return bookingsList
        }
        return;
        },
        getCustomer(id) {
            var customerId;
            for (customerId in this.customers) {
                if (customerId == id - 1) {
                    return this.customers[customerId]
                }
            }
            return;
        },
        getTable(booking_id) {
            var tableId;
            if (!this.bookings[booking_id-1]) {
                return;
            }
            for (tableId in this.tables) {
                if (tableId == this.bookings[booking_id - 1].table - 1) {
                    return this.tables[tableId]
                }
            }
            return;
        },
        delBooking(id) {
            this.$emit('del-booking', id)
        }
    }
}
</script>

<style scoped>
table {
    width: 100%;
}
th {
    text-align: center;
    padding: 10px;
    color: #FFFFFF;
    width: 33%;
}
.td {
    width: 100%;
}
.table_num {
    text-align: center;
    color: #FFFFFF;
}
.cust_num {
    text-align: left;
    color: #FFFFFF;
}
.time-slot {
    background: #f4f4f4;
    padding: 10px;
    border-bottom: 1px #ccc dotted;
    text-align: center;
  }
.headings {
    background: #069799;
    padding: 10px;
}
</style>