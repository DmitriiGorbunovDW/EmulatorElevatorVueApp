<template>
  <div class="floor">
    <div class="boxElevator"></div>
    <div class="boxButton"><button :disabled="this.floorNumber === this.currentFloor" @click="callUp" :class='{
      active: this.isFloorInQueue(this.floorNumber)
    }'>{{ this.floorNumber }}</button></div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex';

export default {
  name: 'Floor',
  props: ['floorNumber'],
  computed: {
    ...mapGetters(['isFloorInQueue', 'elevatorStatus', 'currentFloor'])
  },
  methods: {
    callUp() {
      if (!this.isFloorInQueue(this.floorNumber) && this.elevatorStatus === 'ready') {
        this.$store.commit('addToQueue', this.floorNumber);
        this.$store.commit('changeElevatorStatus', 'active');
      } else if (!this.isFloorInQueue(this.floorNumber)) {
        this.$store.commit('addToQueue', this.floorNumber);
      }
    }
  }
}
</script>

<style>
.floor {
  height: 120px;
  width: 220px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.boxElevator {
  border-bottom: 1px solid black;
  border-right: 1px solid black;
  width: 50%;
  height: 120px;
}

.boxButton {
  width: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.boxButton > button {
  height: 30px;
  width: 30px;
  font-size: 20px;
  cursor: pointer;
  border-radius: 50%;
  border: 1px solid;
  transition: 0.2s ease-in-out;
}

.boxButton > button:hover {
  background-color: orange;
}

.boxButton > .active {
  background-color: orange !important;
}

.elevator {
  height: 120px;
  width: 110px;
  background-color: rgb(48, 213, 200);
  position: absolute;
}

.animate__animated.animate__flash {
  --animate-duration: 3s;
}

</style>