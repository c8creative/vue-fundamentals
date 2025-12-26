<template>
  <div>
    <div class="header">
      <span v-if="open" @click="open = !open">
        <slot name="collapse">&#x25B2; Collapse</slot>
      </span>
      <span v-if="!open" @click="open = !open">
        <slot name="expand">&#x25BC; Expand</slot>
      </span>
    </div>
    <div v-if="open">
      <slot>Default Content</slot>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const open = ref(true);
</script>

<style scoped>
.header {
  background-color: #aaa;
  padding: 3px;
  cursor: pointer;
  font-size: 1.2em;
}
</style>
