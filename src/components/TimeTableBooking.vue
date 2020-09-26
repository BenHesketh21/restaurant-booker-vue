<template>
        <div class="booking"  v-bind:class="{'arrived':booking.arrived}">
            <p class="customer">{{customer.first_name}} {{ customer.last_name }}</p>
            <p class="table">{{ booking.table }}</p>
            <p v-if="!booking.arrived">
            <button class="arrive" v-on:click="bookingArrived">Arrived</button>
            <button class="del" v-on:click="delBooking">X</button>
            </p>
            <p v-else>
            <button class="arrive" v-on:click="bookingArrived">Undo</button>   
            </p>
        </div>
</template>

<script>
export default {
    name: "TimeTableBooking",
    props: ["booking", "customer"],
    methods: {
        bookingArrived() {
            this.booking.arrived = !this.booking.arrived
        },
        delBooking() {
            this.$emit('del-booking', this.booking.id)
        }
    }
    
}
</script>

<style scoped>
.booking {
    background:grey;
    color: white;
    padding: 0px;
    border-bottom: 1px #ccc dotted;
    text-align: left;
    margin-bottom: 0px;
    overflow: hidden;
  }
.customer {
    width: 10%;
    text-align: left;
    padding: 1px;
    margin-top: 17px;
    margin-left: 50px;
    float: left;
    text-decoration-thickness: 100%;
}
.table {
    margin-left: 35%;
    width: 30%;
    text-align: center;
    margin-top: 1%;
    margin-bottom: 1%;
    float: none;
  }

.arrived {
    background: #000000;
}

.arrive {
    background: #71EA6B;
    color: #000000;
    border: none;
    padding: 5px 9px;
    cursor: pointer;
    float: right;
    margin-top: -40px;
    margin-right: 25%;
  }
.del {
    background: #ff0000;
    color: #000000;
    border: none;
    padding: 5px 9px;
    cursor: pointer;
    float: right;
    margin-top: -40px;
    margin-right: 10%;
  }
</style>