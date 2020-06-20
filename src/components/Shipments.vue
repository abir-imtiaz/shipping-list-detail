<template>
  <div>
    <h3>Shipments</h3>
    <input type="text" id="search-bar" v-on:keyup.enter ="$emit('search-id', $event.target.value)" placeholder="Search for ID">
    <table>
      <tr>
        <th v-if="!asc" v-on:click="$emit('sort', 'id', 'asc')">ID</th>
        <th v-else v-on:click="$emit('sort', 'id', 'desc')">ID</th>
        <th v-if="!asc" v-on:click="$emit('sort', 'name', 'asc')">Name</th>
        <th v-else v-on:click="$emit('sort', 'name', 'desc')">Name</th>
        <!--<th>Cargo</th>
        <th>Mode</th>
        <th>Type</th>
        <th>Destination</th>
        <th>Origin</th>
        <th>Services</th>-->
        <th v-if="!asc" v-on:click="$emit('sort', 'total', 'asc')">Total</th>
        <th v-else v-on:click="$emit('sort', 'total', 'desc')">Total</th>
        <th v-if="!asc" v-on:click="$emit('sort', 'status', 'asc')">Status</th>
        <th v-else v-on:click="$emit('sort', 'status', 'desc')">Status</th>
        <!--<th>UserID</th>-->
        <th>Details/Edit</th>
      </tr>
      <tr v-bind:key="shipment.id" v-for="shipment in shipments">
        <td>{{shipment.id}}</td>
        <td>{{shipment.name}}</td>
        <!--<td>{{shipment.cargo}}</td>
        <td>{{shipment.mode}}</td>
        <td>{{shipment.type}}</td>
        <td>{{shipment.destination}}</td>
        <td>{{shipment.origin}}</td>
        <td>{{shipment.services}}</td>-->
        <td>{{shipment.total}}</td>
        <td>{{shipment.status}}</td>
        <!--<td>{{shipment.userId}}</td>-->
        <td><router-link :to="{ name: 'Detail', params: { id: shipment.id }}">...</router-link></td>
      </tr> 
    </table>        

  </div>
</template>

<script>

export default {
  name: "Shipments",
  props: ["shipments", "asc"]
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
  text-align: center;
  padding: 8px;
}

tr:nth-child(even) {
  background-color: #dddddd;
}

#search-bar{
  float: left;
  padding: 6px;
  margin-top: 8px;
  margin-right: 16px;
  font-size: 17px;
}

</style>

