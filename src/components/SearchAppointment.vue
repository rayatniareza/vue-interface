<template>
  <div class="col-12 col-md-10 col-lg-7">
    <div class="input-group my-3">
      <input
        id="SearchApts"
        placeholder="Search"
        type="text"
        class="form-control"
        aria-label="Search Appointment"
        v-model="searchTerm"
      />
      <div class="input-group-append">
        <button
          type="button"
          class="btn btn-primary dropdown-toggle"
          aria-haspopup="true"
          aria-expanded="false"
          data-toggle="dropdown"
        >
          Sort by
          <span class="caret"></span>
        </button>
        <div class="dropdown-menu dropdown-menu-right">
          <a
            href="#"
            class="dropdown-item d-flex justify-content-between"
            id="petName"
            @click="$emit('change-key', 'petName')"
          >
            Pet Name
            <font-awesome-icon icon="check" v-if="myKey === 'petName'" />
          </a>
          <a
            href="#"
            class="dropdown-item d-flex justify-content-between"
            id="aptDate"
            @click="$emit('change-key', 'aptDate')"
          >
            Date
            <font-awesome-icon icon="check" v-if="myKey === 'aptDate'" />
          </a>
          <a
            href="#"
            class="dropdown-item d-flex justify-content-between"
            id="ownerName"
            @click="$emit('change-key', 'petOwner')"
          >
            Owner
            <font-awesome-icon icon="check" v-if="myKey === 'petOwner'" />
          </a>
          <div class="dropdown-divider" role="separator"></div>
          <a
            href="#"
            class="dropdown-item d-flex justify-content-between"
            id="asc"
            @click="$emit('change-dir', 'asc')"
          >
            Asc
            <font-awesome-icon icon="check" v-if="myDir === 'asc'" />
          </a>
          <a
            href="#"
            class="dropdown-item d-flex justify-content-between"
            id="desc"
            @click="$emit('change-key', 'desc')"
          >
            Desc
            <font-awesome-icon icon="check" v-if="myDir === 'desc'" />
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
export default {
  name: "SearchAppointment",
  components: {
    FontAwesomeIcon,
  },
  data() {
    return {
      searchTerm: "",
    };
  },
  props: ["myKey", "myDir"],
  watch: {
    searchTerm: function () {
      this.$emit("search", this.searchTerm);
    },
  },
};
</script>