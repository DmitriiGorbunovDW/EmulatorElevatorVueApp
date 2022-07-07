<template>
  <div class="app">
    <div class="home">
      <Floor v-for="(floor, i) in floors" :key="i" :floorNumber="i + 1" />
      <Elevator />
    </div>
  </div>
</template>

<script>
import Floor from "./components/Floor";
import Elevator from "./components/Elevator";
import useVuelidate from '@vuelidate/core';
import { required, minValue } from '@vuelidate/validators';

export default {
  components: { Floor, Elevator },
  data: () => ({
    amountOfFloors: 5,
    floors: Array(5)
  }),
  setup() {
    return { v$: useVuelidate() };
  },
  validations() {
    return {
      amountOfFloors: { required },
    };
  },
  methods: {
    changeAmountOfFloors() {
      if (this.v$.$invalid) {
        this.v$.$touch();
        return
      }

      this.$store.commit('cleanAll');
      this.floors.length = this.amountOfFloors;
    }
  }
};
</script>