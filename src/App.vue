<template>
  <div id="app">
    <div class="HiltonItemList">
      <HiltonItem v-for="hotel in hotels" :key="hotel.id" :dataHotel="hotel" />
    </div>
    <!-- <HiltonDetails /> -->
  </div>
</template>

<script>
import HiltonItem from '@/components/HiltonItem.vue';
import axios from 'axios';
export default {
  name: 'app',
  components: {
    HiltonItem,
  },
  data() {
    return {
      hotels: null,
    };
  },
  mounted() {
    return axios.get('http://my-json-server.typicode.com/fly365com/code-challenge/hotels').then((response) => {
      this.hotels = response.data;
    });
  },
};
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
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
