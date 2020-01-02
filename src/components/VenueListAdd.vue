<template>
  <div class="col-12 col-md-10 col-lg-8 col-xl-7">
    <div class="card textcenter mt-3" v-if="emptySearch && venues.length == 0">
      <div class="card-header bg-info text-white">
        "
        <span class="font-weight-bold font-italic">{{emptySearch}}</span>
        " could not be found. Enter Venue Details below:
        <!-- <div class="card-header bg-info text-white" @click="hidepanel = !hidepanel"> -->
        <!-- <font-awesome-icon icon="plus" class="mr-3" />Add Venue -->
      </div>

      <div class="card-body">
        <!-- <div class="card-body" :class="{'d-none': hidepanel}"> -->
        <form id="aptForm" @submit.prevent="requestAdd">
          <!-- Venue Name -->
          <div class="form-group form-row">
            <label class="col-md-4 col-form-label text-md-right" for="venueName">Venue Name</label>
            <div class="col-md-8">
              <input
                type="text"
                class="form-control"
                name="venueName"
                id="venueName"
                placeholder="Name of Venue"
                required
                v-model="venueFormData.venueName"
              />
            </div>
          </div>

          <!-- Venue Address Line 01 -->
          <div class="form-group form-row">
            <label class="col-md-4 col-form-label text-md-right" for="venueAddress01">Address Line 1</label>
            <div class="col-md-8">
              <input
                type="text"
                class="form-control"
                id="venueAddress01"
                placeholder="Address 1"
                required
                v-model="venueFormData.venueAddress01"
              />
            </div>
          </div>

          <!-- Venue Address Line 02 -->
          <div class="form-group form-row">
            <label class="col-md-4 col-form-label text-md-right" for="venueAddress02">Address Line 2</label>
            <div class="col-md-8">
              <input
                type="text"
                class="form-control"
                id="venueAddress02"
                placeholder="Address 2"
                v-model="venueFormData.venueAddress02"
              />
            </div>
          </div>

          <div class="form-group form-row">
            <!-- Venue City -->
            <label class="col-md-4 col-form-label text-md-right" for="venueCity">Location/Region</label>
            <div class="col-md-3">
              <input
                type="text"
                class="form-control"
                id="venueCity"
                placeholder
                required
                v-model="venueFormData.venueCity"
              />
            </div>
            <!-- Venue Post Code -->
            <label class="col-md-2 col-form-label text-md-right" for="venuePostcode">Post Code</label>
            <div class="col-md-3">
              <input
                type="text"
                class="form-control"
                id="venuePostcode"
                placeholder="Post Code"
                required
                v-model="venueFormData.venuePostcode"
              />
            </div>
          </div>
          <!-- Add Venue Button -->
          <div class="form-group form-row mb-0">
            <div class="offset-md-2 col-md-10">
              <button type="submit" class="btn btn-info d-block ml-auto">Add Venue</button>
            </div>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
// import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";

export default {
  components: {
    // FontAwesomeIcon
  },
  name: "VenueListAdd",
  props: ["venues", "emptySearch"],
  data() {
    return {
      venueFormData: []
      // hidepanel: true
    };
  },
  methods: {
    requestAdd: function() {
      if (typeof this.venueFormData.venueAddress02 == "undefined") {
        this.venueFormData = {
          venueName: this.venueFormData.venueName,
          venueAddress01: this.venueFormData.venueAddress01,
          venueAddress02: "",
          venueCity: this.venueFormData.venueCity,
          venuePostcode: this.venueFormData.venuePostcode
        };
      } else {
        this.venueFormData = {
          venueName: this.venueFormData.venueName,
          venueAddress01: this.venueFormData.venueAddress01,
          venueAddress02: this.venueFormData.venueAddress02,
          venueCity: this.venueFormData.venueCity,
          venuePostcode: this.venueFormData.venuePostcode
        };
      }
      this.$emit("add", this.venueFormData);
      this.venueFormData = [];
      // this.hidepanel = true;
    }
  }
};
</script>

<style>
.card-header {
  cursor: pointer;
}
</style>