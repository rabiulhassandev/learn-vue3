<!-- Option API -->
<script>
  export default {
    data() {
      return {
        name : "Rabiul Hassan",
        status : 'active',
        items : ['Item 1', 'Item 2', "Item 3"]
      }
    },
    methods: {
      changeStatus() { 
        if(this.status == 'active') this.status = 'inactive'
        else if(this.status == 'inactive') this.status = 'pending'
        else this.status = 'active'
      }
    }
  }

</script>


<template>
  <h1>{{ name }}</h1>
  <h1>the status is <b>{{ status }}</b> </h1>
  <ul>
    <li v-for="item in items" :key="item">{{ item }}</li>
  </ul>
  <button @click="changeStatus">Change Status</button>

</template>