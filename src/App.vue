<template>
  <div id="main-app" class="container">
    <h4>{{ title }}</h4>
    <font-awesome-icon icon="plus" class="mr-2" />Add Appoinment
    <div class="row justify-content-center">
      <appoinment-list
        :appoinments="appoinments"
        @remove="removeItem"
        @edit="editItem"
      />
    </div>
  </div>
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import axios from "axios";
import AppoinmentList from "./components/AppoinmentList";
import _ from "lodash";
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
      aptIndex: 0,
    };
  },
  methods: {
    removeItem: function (apt) {
      //this.appoinments.splice( index, 1 );
      this.appoinments = _.without(this.appoinments, apt);
    },
    editItem: function (id, field, text) {
      const aptIndex = _.findIndex(this.appoinments, {
        aptId: id,
      });
      this.appoinments[aptIndex][field] = text;
    },
  },
  mounted() {
    axios.get("./data/appoinment.json").then(
      (response) =>
        (this.appoinments = response.data.map((item) => {
          item.aptId = this.aptIndex;
          this.aptIndex++;
          return item;
        }))
    );
  },
};
</script>

