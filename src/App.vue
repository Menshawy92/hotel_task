<template>
  <div id="app">
    <div class="HiltonItemList">
      <HiltonItem
        v-bind="{nightsCount}"
        v-for="hotel in hotels"
        :key="hotel.id"
        :dataHotel="hotel"
      />
    </div>
    <HiltonDetails
      v-for="hotel in hotels"
      :key="hotel.id"
      @nights-count-uodated="nightsCount = $event"
      :dataHotel="hotel"
    />
  </div>
</template>

<script>
import HiltonItem from "@/components/HiltonItem.vue";
import HiltonDetails from "@/components/HiltonDetails.vue";
import axios from "axios";
export default {
  name: "app",
  components: {
    HiltonItem,
    HiltonDetails
  },
  data() {
    return {
      hotels: null,
      pricePerNight: null,
      nightsCount: 1,
      detailsHotels: null
    };
  },
  mounted() {
    return axios
      .get(
        "http://my-json-server.typicode.com/fly365com/code-challenge/hotels/"
      )
      .then(response => {
        this.hotels = response.data;
      });
  }
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.HiltonItemList {
  display: flex;
  justify-content: center;
}
</style>
