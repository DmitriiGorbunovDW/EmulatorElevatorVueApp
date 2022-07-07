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

<style>
@import url('https://fonts.googleapis.com/css2?family=Trispace:wght@700&display=swap');

* {
  padding: 0;
  margin: 0;
  font-family: 'Trispace', sans-serif;
}

.app {
  display: flex;
  border: 2px solid black ;
  width: 100%;
  margin: 5px;
}

.app form {
  margin-top: 10px;
}

.app form input {
  width: 27px;
  margin-right: 5px;
}

.app form span {
  font-size: 12px;
  color: red;
}

.home {
  display: flex;
  flex-direction: column-reverse;
}
</style>