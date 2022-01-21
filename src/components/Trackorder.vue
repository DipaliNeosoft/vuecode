<template>
  <div class="container">
      <h1>View/Track order </h1>
      <table class="table table-striped">
  <thead>
      <tr><h3>Welcome {{this.details[0].fullname}}</h3></tr>
    <tr>
      <th scope="col">Order id</th>
      <th scope="col">Full Name</th>
      <th scope="col">Email</th>
      <th scope="col">Address</th>
      <th scope="col">Mobile</th>
      <th scope="col">products</th>
      <th scope="col">total</th>
     
      <th>order status</th>
    </tr>
  </thead>
  <tbody v-for="(order,index) in details" :key="index">
    <tr  >
      <td>{{order.oid}}</td>
      <td>{{order.fullname}}</td>
      <td>{{order.email}}</td>
      <td>Address: {{order.address}}<br> State: {{order.state}}<br> City: {{order.city}} <br> Pincode: {{order.pincode}}</td>
      <td>{{order.mobile}}</td>
      <td> {{order.pname}}</td>
      <td>&#8377; {{order.total_price}}</td>
      <td>{{order.status==0?'Processsing':'Delivered'}}</td>
    </tr>
  </tbody>
</table>
  </div>
</template>

<script>

import { orderDetails } from "@/common/Service";
export default {
  name:"Trackorder",
  data() {
    return {
      uid: localStorage.getItem("user_id"),
    details:[]
    };
  },
  mounted() {
    orderDetails(this.uid)
      .then((res) => {
        this.details = res.data.orders;
       
      })
      .catch((error) => {
        console.log("Something Wrong " + error);
      });
  },
};
</script>

<style>

</style>