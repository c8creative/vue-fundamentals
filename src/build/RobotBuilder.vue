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
        <td class="cost">{{ toCurrency(robot.cost) }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script>
import { computed } from "vue";
import parts from "../data/parts";
import { toCurrency } from "../shared/formatters";

function getNextValidIndex(index, length) {
  const incrementedIndex = index + 1;
  return incrementedIndex >= length ? 0 : incrementedIndex;
}

function getPreviousValidIndex(index, length) {
  const decrementedIndex = index - 1;
  return decrementedIndex < 0 ? length - 1 : decrementedIndex;
}

export default {
  name: "RobotBuilder",
  setup() {
    // 1. Variable declarations (reactive state)
    let availableParts = parts;
    let selectedHeadIndex = 0;
    let selectedLeftArmIndex = 0;
    let selectedTorsoIndex = 0;
    let selectedRightArmIndex = 0;
    let selectedBaseIndex = 0;
    let cart = [];

    // 2. Computed properties
    const selectedRobot = computed(() => {
      return {
        head: availableParts.heads[selectedHeadIndex],
        leftArm: availableParts.arms[selectedLeftArmIndex],
        torso: availableParts.torsos[selectedTorsoIndex],
        rightArm: availableParts.arms[selectedRightArmIndex],
        base: availableParts.bases[selectedBaseIndex],
      };
    });

    // 3. Methods/Functions
    const addToCart = () => {
      const robot = selectedRobot.value;
      const cost =
        robot.head.cost +
        robot.leftArm.cost +
        robot.torso.cost +
        robot.rightArm.cost +
        robot.base.cost;
      cart.push({ ...robot, cost });
      console.log(cart.length);
    };

    //#region selectNext and selectPrevious methods
    const selectNextHead = () => {
      selectedHeadIndex = getNextValidIndex(selectedHeadIndex, availableParts.heads.length);
      console.log("Next head selected");
    };

    const selectPreviousHead = () => {
      selectedHeadIndex = getPreviousValidIndex(selectedHeadIndex, availableParts.heads.length);
      console.log("Previous head selected");
    };

    const selectNextLeftArm = () => {
      selectedLeftArmIndex = getNextValidIndex(selectedLeftArmIndex, availableParts.arms.length);
      console.log("Next left arm selected");
    };

    const selectPreviousLeftArm = () => {
      selectedLeftArmIndex = getPreviousValidIndex(
        selectedLeftArmIndex,
        availableParts.arms.length
      );
      console.log("Previous left arm selected");
    };

    const selectNextTorso = () => {
      selectedTorsoIndex = getNextValidIndex(selectedTorsoIndex, availableParts.torsos.length);
      console.log("Next torso selected");
    };

    const selectPreviousTorso = () => {
      selectedTorsoIndex = getPreviousValidIndex(selectedTorsoIndex, availableParts.torsos.length);
      console.log("Previous torso selected");
    };

    const selectNextRightArm = () => {
      selectedRightArmIndex = getNextValidIndex(selectedRightArmIndex, availableParts.arms.length);
      console.log("Next right arm selected");
    };

    const selectPreviousRightArm = () => {
      selectedRightArmIndex = getPreviousValidIndex(
        selectedRightArmIndex,
        availableParts.arms.length
      );
      console.log("Previous right arm selected");
    };

    const selectNextBase = () => {
      selectedBaseIndex = getNextValidIndex(selectedBaseIndex, availableParts.bases.length);
      console.log("Next base selected");
    };

    const selectPreviousBase = () => {
      selectedBaseIndex = getPreviousValidIndex(selectedBaseIndex, availableParts.bases.length);
      console.log("Previous base selected");
    };
    //#endregion

    // 4. Return statement (exposes to template)
    return {
      availableParts,
      selectedHeadIndex,
      selectedLeftArmIndex,
      selectedTorsoIndex,
      selectedRightArmIndex,
      selectedBaseIndex,
      cart,
      selectedRobot,
      addToCart,
      toCurrency,
      selectNextHead,
      selectPreviousHead,
      selectNextLeftArm,
      selectPreviousLeftArm,
      selectNextTorso,
      selectPreviousTorso,
      selectNextRightArm,
      selectPreviousRightArm,
      selectNextBase,
      selectPreviousBase,
    };
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
