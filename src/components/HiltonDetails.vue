<template>
  <div class="HiltonDetails" v-if="hotel">
    <h2>{{ hotel.name}}</h2>
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
        <img :src="currentPic" alt />
      </div>
      <div class="smallImges">
        <img
          v-for="(image, index) in hotel.pictures"
          :key="index"
          :src="image.thumbnail"
          @click="currentPic = image.photo"
        />
      </div>
    </div>
    <div>
      <p v-for="comment in hotel.reviews" :key="comment.id">{{comment.review}}</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "HiltonDetails",
  data() {
    return {
      nightsCount: 1,
      currentHotel: 0,
      hotel: "",
      currentPic: "",
      comment: ""
    };
  },
  methods: {
    updateNightsCount() {
      this.$emit("nights-count-uodated", this.nightsCount);
    }
  },
  mounted: function() {
    this.$root.eventBus.$on("show-hotel-div", data => {
      axios
        .get(
          "http://my-json-server.typicode.com/fly365com/code-challenge/hotelDetails/" +
            data
        )
        .then(response => {
          this.hotel = response.data;
          this.comment = response.data;
          this.currentPic = this.hotel.pictures[0].photo;
        });
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
