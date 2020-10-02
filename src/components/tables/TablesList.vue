<template>
    <div>
    <table>
        <tr class="headings">
            <th id="table_num">Table Number</th>
            <th id="num_seats">Number of Seats</th>
        </tr>
    </table>
    <div v-bind:key="table.id" v-for="table in tables">
        <TableSlot class="table_slot" v-bind:table="table" v-on:edit-table="editTable" v-on:del-table="$emit('del-table', table.id)" />
    </div>
    </div>
</template>

<script>
import TableSlot from './TableSlot'

export default {
    name: "TablesList",
    components: {
        TableSlot
    },
    props: ["tables"],
    methods: {
        editTable(updatedTable) {
            this.$emit('edit-table', updatedTable)
        }
    }
}
</script>

<style scoped>
.table_slot {
    margin-left: 12.5%;
    margin-right: -100px;
    width: 75%;
}
table {
    width: 75%;
    margin-left: 12.5%;
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
.num_seats {
    text-align: center;
    color: #FFFFFF;
}
.table_num {
    text-align: left;
    color: #FFFFFF;
}
.headings {
    background: #069799;
    padding: 10px;
}
</style>