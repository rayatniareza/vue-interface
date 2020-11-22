<template>
  <div id="main-app" class="container">
    <h4>{{ title }}</h4>
    <font-awesome-icon icon="plus" class="mr-2" />Add Appoinment
    <appoinment-list :appoinments="appoinments" />
  </div>
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import axios from "axios";
import AppoinmentList from "./components/AppoinmentList";

export default {
  name: "MainApp",
  components: {
    FontAwesomeIcon,
    AppoinmentList,
  },
  data: function () {
    return {
      title: "Appointment List",
      appoinments: [],
    };
  },
  mounted() {
    axios
      .get("./data/appoinment.json")
      .then((response) => (this.appoinments = response.data));
  },
};
</script>

