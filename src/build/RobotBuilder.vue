<template>
  <div>
    <div class="top-row">
      <div class="top part">
        <img v-bind:src="availableParts.heads[selectedHeadIndex].imageUrl" alt="head" />
        <button class="prev-selector" v-on:click="selectPreviousHead()">&#9668;</button>
        <button class="next-selector" v-on:click="selectNextHead()">&#9658;</button>
      </div>
    </div>
    <div class="middle-row">
      <div class="left part">
        <img v-bind:src="availableParts.arms[selectedLeftArmIndex].imageUrl" alt="left arm" />
        <button class="prev-selector" v-on:click="selectPreviousLeftArm()">&#9650;</button>
        <button class="next-selector" v-on:click="selectNextLeftArm()">&#9660;</button>
      </div>
      <div class="center part">
        <img v-bind:src="availableParts.torsos[selectedTorsoIndex].imageUrl" alt="torso" />
        <button class="prev-selector" v-on:click="selectPreviousTorso()">&#9668;</button>
        <button class="next-selector" v-on:click="selectNextTorso()">&#9658;</button>
      </div>
      <div class="right part">
        <img v-bind:src="availableParts.arms[selectedRightArmIndex].imageUrl" alt="right arm" />
        <button class="prev-selector" v-on:click="selectPreviousRightArm()">&#9650;</button>
        <button class="next-selector" v-on:click="selectNextRightArm()">&#9660;</button>
      </div>
    </div>
    <div class="bottom-row">
      <div class="bottom part">
        <img v-bind:src="availableParts.bases[selectedBaseIndex].imageUrl" alt="base" />
        <button class="prev-selector" v-on:click="selectPreviousBase()">&#9668;</button>
        <button class="next-selector" v-on:click="selectNextBase()">&#9658;</button>
      </div>
    </div>
  </div>
</template>

<script>
import parts from '../data/parts';

function getNextValidIndex (index, length) {
  const incrementedIndex = index + 1;
  return incrementedIndex >= length ? 0 : incrementedIndex;
}

function getPreviousValidIndex (index, length) {
  const decrementedIndex = index - 1;
  return decrementedIndex < 0 ? length - 1 : decrementedIndex;
}

export default {
  name: 'RobotBuilder',
  data() {
    return { availableParts: parts,
      selectedHeadIndex: 0,
      selectedLeftArmIndex: 0,
      selectedTorsoIndex: 0,
      selectedRightArmIndex: 0,
      selectedBaseIndex: 0,
     };
  },
  methods: {
    selectNextHead() {
      this.selectedHeadIndex = getNextValidIndex(this.selectedHeadIndex, this.availableParts.heads.length);
      console.log('Next head selected');
    },
    selectPreviousHead() {
      this.selectedHeadIndex = getPreviousValidIndex(this.selectedHeadIndex, this.availableParts.heads.length);
      console.log('Previous head selected');
    },
    selectNextLeftArm() {
      this.selectedLeftArmIndex = getNextValidIndex(this.selectedLeftArmIndex, this.availableParts.arms.length);
      console.log('Next left arm selected');
    },
    selectPreviousLeftArm() {
      this.selectedLeftArmIndex = getPreviousValidIndex(this.selectedLeftArmIndex, this.availableParts.arms.length);
      console.log('Previous left arm selected');
    },
    selectNextTorso() {
      this.selectedTorsoIndex = getNextValidIndex(this.selectedTorsoIndex, this.availableParts.torsos.length);
      console.log('Next torso selected');
    },
    selectPreviousTorso() {
      this.selectedTorsoIndex = getPreviousValidIndex(this.selectedTorsoIndex, this.availableParts.torsos.length);
      console.log('Previous torso selected');
    },
    selectNextRightArm() {
      this.selectedRightArmIndex = getNextValidIndex(this.selectedRightArmIndex, this.availableParts.arms.length);
      console.log('Next right arm selected');
    },
    selectPreviousRightArm() {
      this.selectedRightArmIndex = getPreviousValidIndex(this.selectedRightArmIndex, this.availableParts.arms.length);
      console.log('Previous right arm selected');
    },
    selectNextBase() {
      this.selectedBaseIndex = getNextValidIndex(this.selectedBaseIndex, this.availableParts.bases.length);
      console.log('Next base selected');
    },
    selectPreviousBase() {
      this.selectedBaseIndex = getPreviousValidIndex(this.selectedBaseIndex, this.availableParts.bases.length);
      console.log('Previous base selected');
    },
  },
};
</script>

<style>
.part {
  position: relative;
  width: 200px;
  height: 200px;
  border: 3px solid #aaa;
}

.part img {
  width: 200px;
}

.top-row {
  display: flex;
  justify-content: space-around;
}

.middle-row {
  display: flex;
  justify-content: center;
}

.bottom-row {
  display: flex;
  justify-content: space-around;
  border-top: none;
}

.top {
  border-bottom: none;
}

.left {
  border-right: none;
}

.right {
  border-left: none;
}

.left img {
  transform: rotate(-90deg);
}

.right img {
  transform: rotate(90deg);
}

.bottom {
  border-top: none;
}

.prev-selector {
  position: absolute;
  z-index: 1;
  top: -3px;
  left: -28px;
  width: 25px;
  height: 206px;
}

.next-selector {
  position: absolute;
  z-index: 1;
  top: -3px;
  right: -28px;
  width: 25px;
  height: 206px;
}

.center .prev-selector,
.center .next-selector {
  opacity: 0.8;
}

.left .prev-selector {
  top: -28px;
  left: -3px;
  width: 179px;
  height: 25px;
}

.left .next-selector {
  top: auto;
  bottom: -28px;
  left: -3px;
  width: 179px;
  height: 25px;
}

.right .prev-selector {
  top: -28px;
  left: 24px;
  width: 179px;
  height: 25px;
}

.right .next-selector {
  top: auto;
  bottom: -28px;
  left: 24px;
  width: 179px;
  height: 25px;
}

.right .next-selector {
  right: -3px;
}
</style>
