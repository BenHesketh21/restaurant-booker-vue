<template>
    <div>
        <div class="title">
            <h2> When would you like to book?</h2>
        </div>
        <br>
        <form @submit.prevent="isAvailable">
        <input class="date" type="date" v-model="date" :min="today" :max="week">
        <select v-model="time" class="time">
            <option v-bind:key="time" v-for="time in times" :value="time + ':00'">{{ time }}</option>
        </select>
        <br><br>
        <div class="title">
            <h2>How many diners?</h2>
        </div>
        <br>
        <input class="num_of_cust" type="number" v-model="num_of_cust" name="" id="">
        <br><br>
        <input type="submit" value="Check Availability">
        </form>
        <br><br>
        <div v-if="booking.available">
        <svg class="checkmark" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 52 52">
        <circle class="checkmark__circle" cx="26" cy="26" r="25" fill="none"/>
        <path class="checkmark__check" fill="none" d="M14.1 27.2l7.1 7.2 16.7-16.8"/>
        </svg>
            <br>
            <h3>Table {{ booking.table }} is available            
            Would you like to book it?</h3>
            <br><br>
            <button>&#10004;</button>
            <button>X</button>
        </div>
        <div v-else-if="booking.available == false">
            <svg class="cross" version="1.1" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 130.2 130.2">
            <circle class="path circle" fill="none" stroke="#D06079" stroke-width="6" stroke-miterlimit="10" cx="65.1" cy="65.1" r="62.1"/>
            <line class="path line" fill="none" stroke="#fff" stroke-width="6" stroke-linecap="round" stroke-miterlimit="10" x1="34.4" y1="37.9" x2="95.8" y2="92.3"/>
            <line class="path line" fill="none" stroke="#fff" stroke-width="6" stroke-linecap="round" stroke-miterlimit="10" x1="95.8" y1="38" x2="34.4" y2="92.2"/>
            </svg>
            <br>

            <h3>{{ booking.message }}</h3>
        </div>
    </div>
</template>

<script>
export default {
    name: "BookingAvailable",
    props: ['booking'],
    data () {
        return {
            today: this.getToday(),
            week: this.get2WeekAhead(),
            times: ["12:00", "12:30","13:00", "13:30","14:00", "14:30","15:00", "15:30","16:00", "16:30","17:00", "17:30","18:00", "18:30","19:00", "19:30","20:00", "20:30"]
            
        }
    },
    methods: {
        isAvailable() {
            let formattedDate = this.date[8] + this.date[9] + '/' + this.date[5] + this.date[6] + '/' + this.date[0] + this.date[1] + this.date[2] + this.date[3]  
            const requestedBooking = {
                date: formattedDate,
                time: this.time,
                number_of_customers: Number(this.num_of_cust)
            }
            console.log(requestedBooking)
            this.$emit('booking-avail', requestedBooking)
        },
        getToday() {
         let today = new Date().toISOString().slice(0, 10)
            return today;
        },
        get2WeekAhead() {
            let today = new Date()
            today.setDate(today.getDate() + 14)
            let nextWeek = today.toISOString().slice(0, 10)
            // let today = new Date().toLocaleDateString()
            return nextWeek;
        }
    }
}
</script>

<style scoped>
.checkmark__circle {
  stroke-dasharray: 166;
  stroke-dashoffset: 166;
  stroke-width: 2;
  stroke-miterlimit: 10;
  stroke: #7ac142;
  fill: none;
  animation: stroke 0.6s cubic-bezier(0.65, 0, 0.45, 1) forwards;
}

.path.circle{
  stroke-dasharray: 166;
  stroke-dashoffset: 166;
  stroke-width: 2;
  stroke-miterlimit: 10;
  stroke: #D06079;
  fill: none;
  animation: stroke 0.6s cubic-bezier(0.65, 0, 0.45, 1) forwards;
}

.cross {
  width: 56px;
  height: 56px;
  border-radius: 50%;
  display: block;
  stroke-width: 2;
  stroke: #fff;
  stroke-miterlimit: 10;
  margin: 0% auto;
  box-shadow: inset 0px 0px 0px #D06079;
  animation: fill_cross .4s ease-in-out .4s forwards, scale .3s ease-in-out .9s both;
}

.checkmark {
  width: 56px;
  height: 56px;
  border-radius: 50%;
  display: block;
  stroke-width: 2;
  stroke: #fff;
  stroke-miterlimit: 10;
  margin: 0% auto;
  box-shadow: inset 0px 0px 0px #7ac142;
  animation: fill .4s ease-in-out .4s forwards, scale .3s ease-in-out .9s both;
}

.checkmark__check {
  transform-origin: 50% 50%;
  stroke-dasharray: 48;
  stroke-dashoffset: 48;
  animation: stroke 1s cubic-bezier(0.65, 0, 0.45, 1) 0.8s forwards;
}

.path.line {
  transform-origin: 0% 0%;
  stroke-dasharray: 10;
  stroke-dashoffset: 48;
  animation: stroke_cross 1s cubic-bezier(0.65, 2, 0.45, 1) 0.8s forwards;
}
@keyframes stroke_cross {
  100% {
    stroke-dashoffset: -30;
    stroke-dasharray: 0;
  }
}

@keyframes stroke {
  100% {
    stroke-dashoffset: 0;
  }
}
@keyframes scale {
  0%, 100% {
    transform: none;
  }
  50% {
    transform: scale3d(1.1, 1.1, 1);
  }
}
@keyframes fill {
  100% {
    box-shadow: inset 0px 0px 0px 30px #7ac142;
  }
}
@keyframes fill_cross {
  100% {
    box-shadow: inset 0px 0px 0px 30px #D06079;
  }
}
.title {
    background: #f4f4f4;
    padding: 10px;
    border-bottom: 1px #ccc dotted;
    text-align: center;
  }
input {
    width: 20%;
    padding: 10px;
    text-align: center;
    font-size: 1pc;
}
select {
    width: 20%;
    padding: 10px;
    text-align: center;
    font-size: 1pc; 
}
</style>