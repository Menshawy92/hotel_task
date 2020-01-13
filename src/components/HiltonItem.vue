<template>
  <div class="HiltonItem" @click.prevent="showHotelData(dataHotel.id)">
    <h2>{{ dataHotel.name }}</h2>
    <div class="HiltonItem__details">
      <img :src="dataHotel.photo" width="100" alt />
      <div class="conText">
        <ul>
          <li>{{ dataHotel.pricePerNight * nightsCount}} in Night</li>
          <li>{{ dataHotel.totalScore }} Very Good</li>
          <li>{{ dataHotel.totalReviews }} Reviews</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HiltonItem",
  props: {
    dataHotel: {
      required: true
    },
    nightsCount: {
      type: [String, Number]
    }
  },
  data() {
    return {};
  },
  methods: {
    showHotelData: function(hotel_id) {
      this.$root.eventBus.$emit("show-hotel-div", hotel_id);
    }
  }
};
</script>

<style lang="scss">
.HiltonItem {
  margin: 20px;
  width: 300px;
  border: 1px solid #ddd;
  background-color: #fafafa;
  border-radius: 2px;
  cursor: pointer;
  &:hover {
    background-color: #eee;
    transition: all 0.5s;
  }
  h2 {
    border-bottom: 1px solid #ddd;
    padding-bottom: 15px;
  }
  &__details {
    display: flex;
    padding: 20px;
    img {
      background-color: #fff;
      padding: 7px;
      border: 1px solid #ddd;
      border-radius: 3px;
    }
    .conText {
      width: 100%;
      ul {
        list-style: none;
        padding: 0;
        li {
          font-weight: bold;
          border-bottom: 1px solid #ddd;
          padding-bottom: 6px;
          margin-bottom: 6px;
          text-align: left;
          padding-left: 15px;
          &:last-child {
            border-bottom: 0;
          }
        }
      }
    }
  }
}
</style>
