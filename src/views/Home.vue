<template>
  <div class="home">
    <Shipments v-bind:shipments="shipments" v-bind:asc="asc" v-on:search-id="searchID" v-on:sort="sortCol"/>
  </div>
</template>

<script>
import Shipments from '../components/Shipments';
import axios from 'axios';

export default {
  name: 'Home',
  components: {
    Shipments,
  },
  data() {
    return {
      shipments: [],
      asc: false
    }
  },
  methods: {
    searchID(id) {
      if(id){
        axios.get(`http://localhost:3000/shipments?id=${id}`)
        .then(res => this.shipments = res.data)
        .catch(err => console.log(err));
      }else{
        axios.get('http://localhost:3000/shipments?_limit=20')
        .then(res => this.shipments = res.data)
        .catch(err => console.log(err));
      }
    },
    sortCol(field, order){
      axios.get(`http://localhost:3000/shipments?_sort=${field}&_order=${order}&_limit=20`)
      .then(res => this.shipments = res.data)
      .catch(err => console.log(err));
      if (order=='asc') {
        console.log('here');
        this.asc= true
      } else {
        this.asc= false
      }
    }
  },
  created() {
    axios.get('http://localhost:3000/shipments?_page=1&_limit=20')
    .then(res => this.shipments = res.data)
    .catch(err => console.log(err));
  }
}
</script>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
  }
</style>