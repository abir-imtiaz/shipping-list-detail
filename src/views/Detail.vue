<template>
  <div class="Detail">
    <ShipItem v-bind:shipitem="shipitem" v-bind:editMode="editMode" v-on:edit-inline="editInline" v-on:updateName="updateInline"/>
    
  </div>
</template>

<script>
import ShipItem from '../components/ShipItem';
import axios from 'axios';

export default {
  name: 'Detail',
  components: {
    ShipItem,
  },
  data() {
    return {
      shipitem: [],
      editMode: false
    }
  },
  methods: {
      editInline() {
        this.editMode= true
      },
      updateInline(updateVal){
        const { id, val} = updateVal;
        axios.patch(`http://localhost:3000/shipments/${id}/`,{name: val})
        .then(res => this.shipitem = [...this.shipitem, res.data])
        .catch(err => console.log(err));
        this.editMode= false
      }
  },
  created() {
    axios.get(`http://localhost:3000/shipments/${this.$route.params.id}`)
    .then(res => this.shipitem = res.data)
    .catch(err => console.log(err));
  }
}
</script>

<style scoped>

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