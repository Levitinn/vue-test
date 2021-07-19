<template>
  <div id="app">
    <StaffTable />
  </div>
</template>

<script>
import StaffTable from './components/StaffTable/StaffTable.vue'

export default {
  name: 'App',
  components: {
    StaffTable
  }
}
</script>

<style>
  * {
        box-sizing: border-box;
    }
    body {
        background-color: #f5f6f8;
    }
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        color: #2c3e50;
        margin-top: 60px;
    }
    .table-wrapper {
        display: flex;
        justify-content: center;  
        flex-direction: column;
        max-width: 700px;
        margin: 0 auto
    }
    .base-btn {
        border-radius: 16px;
        width: 200px;
        padding: 7px;
        cursor: pointer;
    }
    .base-input {
        padding: 3px 4px;
        width: 200px;
    }
</style>
