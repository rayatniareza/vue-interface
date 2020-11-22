<template>
  <div id="main-app" class="container">
    <!-- <h4>{{ title }}</h4>
    <font-awesome-icon icon="plus" class="mr-2" />Add Appointment -->
    <div class="row justify-content-center">
      <add-appointment @add="addItem" />
      <appointment-list
        :appointments="appointments"
        @remove="removeItem"
        @edit="editItem"
      />
    </div>
  </div>
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import axios from "axios";
import AppointmentList from "./components/AppointmentList";
import _ from "lodash";
import AddAppointment from "./components/AddAppointment";
export default {
  name: "MainApp",
  components: {
    FontAwesomeIcon,
    AppointmentList,
    AddAppointment,
  },
  data: function () {
    return {
      title: "Appointment List",
      appointments: [],
      aptIndex: 0,
    };
  },
  methods: {
    addItem: function (apt) {
      apt.aptId = this.aptIndex;
      this.aptIndex++;
      this.appointments.push(apt);
    },
    removeItem: function (apt) {
      //this.appoinments.splice( index, 1 );
      this.appointments = _.without(this.appointments, apt);
    },
    editItem: function (id, field, text) {
      const aptIndex = _.findIndex(this.appointments, {
        aptId: id,
      });
      this.appointments[aptIndex][field] = text;
    },
  },
  mounted() {
    axios.get("./data/appoinment.json").then(
      (response) =>
        (this.appointments = response.data.map((item) => {
          item.aptId = this.aptIndex;
          this.aptIndex++;
          return item;
        }))
    );
  },
};
</script>

