<template>
  <div class="col-12 col-md-10 col-lg-8 col-xl-7">
    <div class="list-group list-group-flush" v-if="emptySearch">
      <div
        class="list-group-item d-flex align-items-start"
        v-for="item in venues"
        :key="item.venueIndexId"
      >
        <div class="w-100">
          <span class="h5 text-info">{{item.venueName}}</span>
          <div class="address">
            {{item.venueAddress01}},
            <span v-if="item.venueAddress02">{{item.venueAddress02}},</span>
            {{item.venueCity}}, {{item.venuePostcode}}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "VenueList",
  props: ["venues", "emptySearch"]
};
</script>