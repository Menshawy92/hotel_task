<template>
  <div class="HiltonDetails" v-if="currentHotel == hotel.id">
    <h2>Hilton Sharm</h2>
    <div class="selectNights">
      <strong>For</strong>
      <select @change="updateNightsCount" v-model="nightsCount">
        <option value>1</option>
        <option>2</option>
        <option>3</option>
        <option>4</option>
        <option>5</option>
        <option>6</option>
      </select>
      <strong>Nights</strong>
    </div>
    <div class="slideShow">
      <div class="bigImage">
        <img :src="dataHotel.pictures[0].photo" alt />
      </div>
      <div class="smallImges">
        <img :src="dataHotel.pictures[0].thumbnail" v-for="image in dataHotel" :key="image" alt />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HiltonDetails",
  props: {
    cost: {
      type: String
    },
    hotel: {
      required: true
    }
  },
  data() {
    return {
      dataHotel: "",
      nightsCount: 1,
      currentHotel: 0
    };
  },
  methods: {
    updateNightsCount() {
      this.$emit("nights-count-uodated", this.nightsCount);
    }
  },
  mounted: function() {
    this.$root.eventBus.$on("show-hotel-div", data => {
      this.currentHotel = data;
    });
  }
};
</script>

<style lang="scss">
.HiltonDetails {
  border-top: 1px solid #ddd;
  margin-top: 20px;
  padding-top: 20px;
  h2 {
    text-transform: uppercase;
    font-size: 40px;
    color: green;
    font-weight: bold;
  }
  .slideShow {
    margin-top: 30px;
    .bigImage {
      img {
        width: 1000px;
        height: 500px;
        object-fit: cover;
        background-color: #fff;
        padding: 15px;
        border: 1px solid #ddd;
        border-radius: 3px;
        box-shadow: 0px 0px 6px 2px #dddd;
      }
    }
    .smallImges {
      img {
        width: 150px;
        height: 100px;
        object-fit: cover;
        background-color: #fff;
        padding: 5px;
        border: 1px solid #ddd;
        border-radius: 3px;
        margin: 10px;
        cursor: pointer;
        &:hover {
          opacity: 0.7;
          transition: all 0.5s;
        }
      }
    }
  }
  .selectNights {
    display: flex;
    align-items: center;
    justify-content: center;
    strong {
      margin: 10px;
    }
    select {
      width: 80px;
      height: 30px;
      font-size: 20px;
      text-align: center;
    }
  }
}
</style>
