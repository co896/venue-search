<template>
  <div id="main-app" class="container">
    <div class="row justify-content-center">
      <venue-list-search
        @searchRecords="searchVenues"
        :selectedKey="filterKey"
        :selectedDir="filterDir"
        @requestKey="requestSearchKey"
        @requestDir="requestSearchDir"
      />
    </div>
    <div class="row justify-content-center">
      <venue-list-add @add="addVenue" :venues="filteredVenues" :emptySearch="searchVenueList" />
    </div>
    <div class="row justify-content-center">
      <venue-list :venues="filteredVenues" :emptySearch="searchVenueList" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import _ from "lodash";
import VenueList from "./components/VenueList";
import VenueListAdd from "./components/VenueListAdd";
import VenueListSearch from "./components/VenueListSearch";

export default {
  components: {
    VenueList,
    VenueListAdd,
    VenueListSearch
  },
  name: "MainApp",
  data() {
    return {
      venues: [],
      venueIndex: 0,
      searchVenueList: "",
      filterKey: "venueName",
      filterDir: "asc"
    };
  },
  mounted() {
    axios.get("./data/venues.json").then(
      response =>
        (this.venues = response.data.map(item => {
          item.venueIndexId = this.venueIndex;
          this.venueIndex++;
          return item;
        }))
    );
  },
  computed: {
    searchedVenues: function() {
      return this.venues.filter(item => {
        return (
          item.venueName
            .toLowerCase()
            .match(this.searchVenueList.toLowerCase()) ||
          item.venueAddress01
            .toLowerCase()
            .match(this.searchVenueList.toLowerCase()) ||
          item.venueAddress02
            .toLowerCase()
            .match(this.searchVenueList.toLowerCase()) ||
          item.venueCity
            .toLowerCase()
            .match(this.searchVenueList.toLowerCase()) ||
          item.venuePostcode
            .toLowerCase()
            .match(this.searchVenueList.toLowerCase())
        );
      });
    },
    filteredVenues: function() {
      return _.orderBy(
        this.searchedVenues,
        item => {
          return item[this.filterKey].toLowerCase();
        },
        this.filterDir
      );
    }
  },
  methods: {
    addVenue: function(newVenue) {
      newVenue.venueIndexId = this.venueIndex;
      this.venueIndex++;
      this.venues.push(newVenue);
      this.searchVenueList = newVenue.venueName;
    },
    searchVenues: function(newSearch) {
      this.searchVenueList = newSearch;
    },
    requestSearchKey: function(chosenKey) {
      this.filterKey = chosenKey;
    },
    requestSearchDir: function(chosenDir) {
      this.filterDir = chosenDir;
    }
  }
};
</script>

<style>
</style>
