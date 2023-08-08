<script setup lang="ts">
import defaultLayout from './components/ui/layouts/defaultLayout.vue';
import previewView from './components/ui/views/previewView.vue';
</script>

<template>
  <defaultLayout>
    <template #actionbar>
      <button>Play</button>
    </template>
    <template #left-area>
      <previewView />
    </template>
    <template #center-area>
      <div>flowview</div>
    </template>
    <template #right-area>
      <div>inspector</div>
    </template>
  </defaultLayout>
</template>

<style>

</style>
