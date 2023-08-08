<script setup lang="ts">
import { Ref, onMounted, ref } from 'vue';

const canvasWidth = ref(1080);
const canvasHeight = ref(1920);
const scale = ref(0.35);
const scaleMax = 2;
const scaleMin = 0.1;
const scaleStep = 0.05;
const gameViewWrapper = ref<HTMLDivElement | null>(null);

onMounted(() => {
  setCanvasToCenter();
})

const scaleUp = function() {
  let s = Math.floor((scale.value * 100) / (scaleStep*100)) * scaleStep + scaleStep;
  if (s > scaleMax) s = scaleMax;
  scale.value = s;
  setCanvasToCenter();
}

const scaleDown = function() {
  let s = Math.floor((scale.value * 100) / (scaleStep * 100)) * scaleStep - scaleStep;
  if (s < scaleMin) s = scaleMin;
  scale.value = s;
  setCanvasToCenter();
}

const setCanvasToCenter = function() {
  const gvw = gameViewWrapper.value;
  if (gvw) {
    gvw.scrollTop = gvw.scrollHeight / 2 - (canvasHeight.value * scale.value) / 2 - (gvw.clientHeight - (canvasHeight.value * scale.value)) / 2;
    gvw.scrollLeft = gvw.scrollWidth / 2 - (canvasWidth.value * scale.value) / 2 - (gvw.clientWidth - (canvasWidth.value * scale.value)) / 2;
  }
}

</script>

<template>
  <div class="preview-view-wrapper">
    <div class="funcbar">
      <span>{{ Math.round(scale * 100) }} %</span>
      <button @click="scaleDown">-</button>
      <input v-model="scale" type="range" min="0.1" max="2" step="0.01" @input="setCanvasToCenter">
      <button @click="scaleUp">+</button>
      <button @click="setCanvasToCenter">center</button>
    </div>
    <div class="game-view-wrapper" ref="gameViewWrapper">
      <div class="game-view"
        :style="{
          'width': `${canvasWidth}px`, 
          'height': `${canvasHeight}px`,
          'transform': `scale(${scale})`,
        }"
      >
      </div>
    </div>
  </div>
</template>

<style lang="scss">
.preview-view-wrapper {
  --funcbar-height: 25px;

  display: flex;
  flex-direction: column;

  .funcbar {
    position: relative;
    width: 450px;
    height: var(--funcbar-height);
    background-color: #222;
    flex-shrink: 0;
    border-bottom: 1px solid #444;
  }

  .game-view-wrapper {
    position: relative;
    justify-content: center;
    align-items: center;
    width: 450px;
    height: calc(100vh - var(--actionbar-height) - var(--funcbar-height));
    background: var(--main-bg-color);
    // background-color: orange;
    overflow: auto;

    .game-view {
      background-color: #000;
      border: 1px solid #888;
      translate: 0.2s;
      border-radius: 50px;
    }
  }
}
</style>
