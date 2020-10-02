<template>
	<div>
        <TimeTableDay v-on:date="whichDate" />
        <div v-bind:key="time.id" v-for="time in times">
        <TimeTableSlot v-bind:time="time" v-bind:bookings="bookings" v-bind:customers="customers" v-bind:tables="tables" v-on:del-booking="delBooking" v-bind:date="date" />
        </div>
	</div>
</template>


<script>
import TimeTableSlot from './TimeTableSlot';
import TimeTableDay from './TimeTableDay';

export default {
    name: "TimeTable",
    components: {
        TimeTableSlot,
        TimeTableDay
    },
    props: ["bookings", "customers", "tables"],
    data () {
        return {
            times: this.timeslots(),
            date: this.getToday()
        }
    },
    methods:{
        timeslots() {
            let full_times = []
            let times = ["12:00:00", "12:30:00","13:00:00", "13:30:00","14:00:00", "14:30:00","15:00:00", "15:30:00","16:00:00", "16:30:00","17:00:00", "17:30:00","18:00:00", "18:30:00","19:00:00", "19:30:00","20:00:00", "20:30:00"]
            var time;
            for (time in times) {
                full_times.push({
                    id:time,
                    time:times[time]
                })
            }
            return full_times
        },
        delBooking(id) {
            this.$emit('del-booking', id)
        },
        whichDate(date) {
            this.date = date
        },
        getToday() {
            var today = new Date();
            var dd = String(today.getDate()).padStart(2, '0');
            var mm = String(today.getMonth() + 1).padStart(2, '0'); //January is 0!
            var yyyy = today.getFullYear();

            today = dd + '/' + mm + '/' + yyyy;
            return today;
        }
    }
}
</script>

<style>
	.bar > input, select {
		display: inline-block;
		width: 8em;
		border: 1px solid #ddd;
		border-radius:  5px;
		padding: 0.2rem 1em;
		margin: 1em;
	}
	button {
		border: 2px solid #ddd;
		background-color: transparent;
		border-radius: 5px;
		padding: .5rem 2em;
		margin: 1em;
	}
</style>