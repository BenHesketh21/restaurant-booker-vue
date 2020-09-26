<template>
  <div class="tables">
    <TablesList v-bind:tables="tables" v-on:del-table="delTable" v-on:edit-table="editTable" />
    <br>
    <NewTable v-on:add-table="addTable" />
  </div>
</template>

<script>
import TablesList from '../components/TablesList' 
import NewTable from '../components/NewTable'

export default {
  name: "Tables",
  components: {
    TablesList,
    NewTable
  },
  data () {
    return {
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
      ]
    }
  },
  methods: {
    addTable(newTable) {
      this.tables = [...this.tables, newTable]
    },
    delTable(id) {
      this.tables = this.tables.filter(table => table.id!=id)
    },
    getTableIds() {
      var ids = []
      var table
      for (table in this.tables) {
        ids.push(Number(this.tables[table].id))
      }
      return ids
    },
    getTable(id) {
      var table;
      for (table in this.tables) {
        if (this.tables[table].id == id) {
          return this.tables.indexOf(this.tables[table])
        }
      }
    },
    editTable(updatedTable) {
      var ids = this.getTableIds()
      var id
      for (id in ids) {
        console.log(id)
        if (ids[id] == updatedTable.id) {
          this.tables[this.getTable(ids[id])].number_of_seats = Number(updatedTable.number_of_seats)
          console.log(this.tables[this.getTable(id)])
        }
      }
    }
  }
}
</script>

<style scoped>

</style>