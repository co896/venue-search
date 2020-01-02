<template>
  <div class="col-12 col-md-10 col-lg-8 col-xl-7">
    <div class="input-group my-3">
      <input
        id="SearchApts"
        placeholder="Search for a Venue"
        type="text"
        class="form-control"
        aria-label="Search Appointments"
        v-model="searchTerm"
      />

      <div class="input-group-append">
        <button
          type="button"
          class="btn btn-info dropdown-toggle"
          data-toggle="dropdown"
          aria-haspopup="true"
          aria-expanded="false"
        >
          Sort by
          <span class="caret"></span>
        </button>

        <div class="dropdown-menu dropdown-menu-right">
          <a
            href="#"
            class="dropdown-item d-flex justify-content-between"
            id="venueName"
            @click="$emit('requestKey', 'venueName')"
          >
            Venue Name
            <font-awesome-icon icon="check" v-if="selectedKey==='venueName'" />
          </a>

          <a
            class="dropdown-item d-flex justify-content-between"
            href="#"
            id="venueCity"
            @click="$emit('requestKey', 'venueCity')"
          >
            Location
            <font-awesome-icon icon="check" v-if="selectedKey==='venueCity'" />
          </a>

          <a
            href="#"
            class="dropdown-item d-flex justify-content-between"
            id="venuePostcode"
            @click="$emit('requestKey', 'venuePostcode')"
          >
            Post Code
            <font-awesome-icon icon="check" v-if="selectedKey==='venuePostcode'" />
          </a>

          <div class="dropdown-divider" role="separator"></div>

          <a
            class="dropdown-item d-flex justify-content-between"
            href="#"
            id="asc"
            @click="$emit('requestDir', 'asc')"
          >
            Asc
            <font-awesome-icon icon="check" v-if="selectedDir==='asc'" />
          </a>

          <a
            class="dropdown-item d-flex justify-content-between"
            href="#"
            id="desc"
            @click="$emit('requestDir', 'desc')"
          >
            Desc
            <font-awesome-icon icon="check" v-if="selectedDir==='desc'" />
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";

export default {
  components: {
    FontAwesomeIcon
  },
  name: "VenueListSearch",
  props: ["selectedKey", "selectedDir"],
  data() {
    return {
      searchTerm: ""
    };
  },
  watch: {
    searchTerm: function() {
      this.$emit("searchRecords", this.searchTerm);
    }
  }
};
</script>