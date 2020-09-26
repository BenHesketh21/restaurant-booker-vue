<template>
    <div>
        <form @submit.prevent="addTable">
        <input type="number" v-model="id" class="table_num" name="table_number" id="table-id">
        <input type="number" v-model="seats" class="num_seats" name="number_of_seats" id="number-of-seats">
        <br><br><input type="submit" value="Add">
        </form>
    </div>
</template>

<script>
export default {
    name: "New Table",
    data() {
        return {
            id: '',
            seats: ''
        }
    },
    methods: {
        addTable() {
             const newTable = {
                 id: this.id,
                 number_of_seats: this.seats
             }
             this.$emit('add-table', newTable);
             this.id = "";
             this.seats = "";
        }
    }
}
</script>

<style scoped>
input {
    width: 22%;
    padding: 10px;
    text-align: center;
    font-size: 1pc;
}


</style>