<script setup lang="ts">
import defaultLayout from './components/ui/layouts/defaultLayout.vue'
</script>

<template>
  <div class="default-layout">
    <div class="actionbar">
      <slot name="actionbar"></slot>
    </div>
    <div class="area-wrapper">
      <div class="left-area">
        <slot name="left-area"></slot>
      </div>
      <div class="center-area">
        <slot name="center-area"></slot>
      </div>
      <div class="right-area">
        <slot name="right-area"></slot>
      </div>
    </div>
  </div>
</template>

<style lang="scss">
.default-layout {
  display: flex;
  flex-direction: column;
  position: absolute;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  color: #fff;
  background-color: #222;

  .actionbar {
    flex-shrink: 0;
    background: #000;
    height: 50px;
  }
  .area-wrapper {
    flex-grow: 1;
    display: flex;
    flex-direction: row;

    .left-area {
      flex-grow: 0;
      overflow: hidden;
      width: 450px;
    }
    .center-area {
      flex-grow: 1;
      border-left: 1px solid #444;
      overflow: hidden;
    }
    .right-area {
      width: 370px;
      border-left: 1px solid #444;
      overflow: hidden;
    }
  }
}
</style>
