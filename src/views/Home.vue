<template>
    <div id="app">
      <TimeTable v-bind:bookings="bookings" v-bind:customers="customers" v-bind:tables="tables" v-on:del-booking="delBooking" />
    </div>
</template>

<script>
import TimeTable from '../components/TimeTable';

export default {
  name: 'Home',
  components: {
    TimeTable
  },
  data () {
    return {
      bookings: [
        {
          id: 1,
          time:"12:00:00",
          date:"12/09/2020",
          table:1,
          user:1,
          arrived: false
        },
        {
          id: 2,
          time:"15:30:00",
          date:"12/09/2020",
          table:2,
          user:1,
          arrived: false
        },
        {
          id: 3,
          time:"12:00:00",
          date:"12/09/2020",
          table:3,
          user:2,
          arrived: false
        },
        {
          id: 4,
          time:"16:30:00",
          date:"12/09/2020",
          table:1,
          user:2,
          arrived: false
        },
        {
          id: 5,
          time:"12:30:00",
          date:"12/09/2020",
          table:3,
          user:3,
          arrived: false
        },
        {
          id: 6,
          time:"12:30:00",
          date:"12/09/2020",
          table:1,
          user:1,
          arrived: false
        },
        {
          id: 7,
          time:"12:30:00",
          date:"12/09/2020",
          table:2,
          user:1,
          arrived: false
        },
        {
          id: 8,
          time:"12:00:00",
          date:"12/09/2020",
          table:2,
          user:2,
          arrived: false
        },
        {
          id: 9,
          time:"12:00:00",
          date:"12/09/2020",
          table:4,
          user:2,
          arrived: false
        }       
      ],
      tables: [
        {
          id: 1,
          number_of_seats:1
        },
        {
          id: 2,
          number_of_seats:2
        },
        {
          id: 3,
          number_of_seats:3
        },
        {
          id: 4,
          number_of_seats:4
        }
      ],
      customers: [
        {
          id:1,
          first_name: "Ben",
          last_name: "Hesketh",
          email: "heskethben0@gmail.com",
          staff: false
        },
        {
          id:2,
          first_name: "Luke",
          last_name: "Benson",
          email: "luke@luke.com",
          staff: false
        },
        {
          id:3,
          first_name: "Lauren",
          last_name: "Stocks",
          email: "lauren@stocks.com",
          staff: false
        }
      ]
    }
  },
  methods: {
    delBooking(id) {
      this.bookings = this.bookings.filter(bookings => bookings.id!=id)
    }
  }
}
</script>

<style scoped>

</style>