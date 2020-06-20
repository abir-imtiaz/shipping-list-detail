<template>
  <div>
    <h3>Shipment - {{shipitem.id}}</h3>
    <router-link to="/" id="back-btn" tag="button">Go Back</router-link>
    <table>
        <tr>
            <th>ID</th>
            <td>{{shipitem.id}}</td>
        </tr>
        <tr v-if="!editMode" v-on:click="$emit('edit-inline')">
            <th>Name</th>
            <td>{{shipitem.name}}</td>
        </tr>
        <tr v-else v-on:keyup.enter="updateName()">
            <th>Name</th>
            <td><input v-model="shipitem.name"></td>
        </tr>
        <tr>
            <th>Cargo</th>
            <td>
                <tr>
                  <th>Item</th>
                  <th>Type</th>
                  <th>Description</th>
                  <th>Volume</th>
                </tr>
                <tr v-for="(item, index) in shipitem.cargo" :key="item.index">
                  <td>{{index}}</td>
                  <td>{{item.type}}</td>
                  <td>{{item.description}}</td>
                  <td>{{item.volume}}</td>
                </tr>
            </td>
        </tr>
        <tr>
            <th>Mode</th>
            <td>{{shipitem.mode}}</td>
        </tr>
        <tr>
            <th>Type</th>
            <td>{{shipitem.type}}</td>
        </tr>
        <tr>
            <th>Destination</th>
            <td>{{shipitem.destination}}</td>
        </tr>
        <tr>
            <th>Origin</th>
            <td>{{shipitem.origin}}</td>
        </tr>
        <tr>
            <th>Status</th>
            <td>{{shipitem.status}}</td>
        </tr>
        <tr>
            <th>Services</th>
            <td>
                <tr>
                  <th>Item</th>
                  <th>Type</th>
                  <th>Value</th>
                </tr>
                <tr v-for="(item, index) in shipitem.services" :key="item.index">
                  <td>{{index}}</td>
                  <td>{{item.type}}</td>
                  <td>{{item.value}}</td>
                </tr>
            </td>
        </tr>
        <tr>
            <th>Total</th>
            <td>{{shipitem.total}}</td>
        </tr>
        <tr>
            <th>UserID</th>
            <td>{{shipitem.userId}}</td>
        </tr>
    </table> 
  </div>
</template>

<script>

export default {
  name: "ShipItem",
  props: ["shipitem", "editMode"],
  data() {
    return {
      title: ''
    }
  },
  methods: {
    updateName() {
      const updateVal = {
        id: this.shipitem.id,
        val: this.shipitem.name,
      }
      // Send up to parent
      this.$emit('updateName', updateVal);
    }
  }
}
</script>

<style scoped>

  table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
  }

  td, th {
    border: 1px solid #dddddd;
    text-align: left;
    padding: 8px;
  }

  tr:nth-child(even) {
    background-color: #dddddd;
  }

  #back-btn{
    background-color: #555555;
    border: none;
    color: white;
    padding: 10px 24px;
    text-align: left;
    text-decoration: none;
    font-size: 14px;
    float: left;
  } 

  input {
    width: 50%;
    padding: 6px 8px;
    margin: 4px 0;
    box-sizing: border-box;
  }

</style>