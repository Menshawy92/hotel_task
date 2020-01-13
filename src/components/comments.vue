<template>
  <div class="comments">
    <div class="item" v-for="hotel in hotelsData" :key="hotel.id">
      <p v-for="(data, index) in hotel.reviews" :key="index">{{data.review}} {{data.score}}</p>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "comments",
  data() {
    return {
      hotelsData: []
    };
  },
  mounted() {
    return axios
      .get(
        "http://my-json-server.typicode.com/fly365com/code-challenge/hotelDetails"
      )
      .then(response => {
        this.hotelsData = response.data;
      });
  }
};
</script>
<style lang="scss">
.comments {
  max-width: 800px;
  margin: auto;
  .item {
    display: flex;
    align-items: center;
    span {
      width: 40px;
      height: 40px;
      display: flex;
      align-items: center;
      justify-content: center;
      background-color: red;
      border-radius: 50%;
      color: #fff;
      margin-right: 10px;
    }
    p {
      text-align: left;
    }
  }
}
</style>