<template>
  <div class="content">
    <button class="add-to-cart" @click="addToCart">Add to Cart</button>
    <div class="top-row">
      <div class="top part">
        <div class="robot-name">
          {{ selectedRobot.head.title }} Bot
          <span v-if="selectedRobot.head.onSale" class="sale">Sale!</span>
          </div>
        <img :src="selectedRobot.head.imageUrl" alt="head" />
        <button class="prev-selector" @click="selectPreviousHead()">&#9668;</button>
        <button class="next-selector" @click="selectNextHead()">&#9658;</button>
      </div>
    </div>
    <div class="middle-row">
      <div class="left part">
        <img :src="selectedRobot.leftArm.imageUrl" alt="left arm" />
        <button class="prev-selector" @click="selectPreviousLeftArm()">&#9650;</button>
        <button class="next-selector" @click="selectNextLeftArm()">&#9660;</button>
      </div>
      <div class="center part">
        <img :src="selectedRobot.torso.imageUrl" alt="torso" />
        <button class="prev-selector" @click="selectPreviousTorso()">&#9668;</button>
        <button class="next-selector" @click="selectNextTorso()">&#9658;</button>
      </div>
      <div class="right part">
        <img :src="selectedRobot.rightArm.imageUrl" alt="right arm" />
        <button class="prev-selector" @click="selectPreviousRightArm()">&#9650;</button>
        <button class="next-selector" @click="selectNextRightArm()">&#9660;</button>
      </div>
    </div>
    <div class="bottom-row">
      <div class="bottom part">
        <img :src="selectedRobot.base.imageUrl" alt="base" />
        <button class="prev-selector" @click="selectPreviousBase()">&#9668;</button>
        <button class="next-selector" @click="selectNextBase()">&#9658;</button>
      </div>
    </div>
  </div>
  <h1>Cart</h1>
  <table>
    <thead>
      <tr>
        <th>Robot</th>
        <th class="cost">Cost</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(robot, index) in cart" :key="index">
        <td>{{ robot.head.title }} Bot</td>
        <td class="cost">${{ robot.cost }}</td>
      </tr>
    </tbody>
  </table>
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
      cart: [],
     };
  },
  computed: {
    selectedRobot() {
      return {
        head: this.availableParts.heads[this.selectedHeadIndex],
        leftArm: this.availableParts.arms[this.selectedLeftArmIndex],
        torso: this.availableParts.torsos[this.selectedTorsoIndex],
        rightArm: this.availableParts.arms[this.selectedRightArmIndex],
        base: this.availableParts.bases[this.selectedBaseIndex],
      };
    },
  },
  methods: {
    addToCart() {
      const robot = this.selectedRobot;
      const cost = robot.head.cost + robot.leftArm.cost + robot.torso.cost + robot.rightArm.cost + robot.base.cost;
      this.cart.push({ ...robot, cost });
      console.log(this.cart.length);
    },
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

.robot-name {
  position: absolute;
  top: -25px;
  text-align: center;
  width: 100%;
}
.sale {
  color: red;
  font-weight: bold;
  margin-left: 5px;
}
.content {
  position: relative;
}
.add-to-cart {
  position: absolute;
  top: 0;
  right: 0;
  z-index: 2;
  padding: 10px 20px;
  font-size: 16px;
  background-color: #28a745;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}
td,
th {
  padding: 10px;
  border-bottom: 1px solid #ddd;
}
</style>
