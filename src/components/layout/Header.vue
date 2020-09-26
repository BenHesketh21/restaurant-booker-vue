<template>
  <header class="header">
    <h1>Booker</h1>
    <div id="nav">
        | <router-link to="/">Timetable</router-link>| 
        <router-link to="/tables">Tables</router-link>|
    </div>
  </header>
</template>

<script>
import router from '../../router';

export default {
  name: "Header",
  data () {
    return {
      router: router
    }
  }
}
</script>

<style scoped>
  .header {
    background: #000200;
    color: #fff;
    text-align: center;
    padding: 10px;
  }
  .header a {
    color: #fff;
    padding-right: 5px;
    text-decoration: none;
  }
</style>