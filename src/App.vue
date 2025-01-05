<script setup lang="ts">
import { ref } from 'vue';
import MainFolder from './components/MainFolder.vue'
import SubFolder from './components/SubFolder.vue'
import File from './components/File.vue'

const currentFolder = ref<number | null>(null);
const currentSubFolder = ref<number | null>(null);

const showSub = (folderId: number) => {
  currentFolder.value = folderId;
};

const showFile = (subFolderId: number) => {
  currentSubFolder.value = subFolderId;
};

</script>

<template>
  <main>
    <div class="row">
      <div class="col lg-4">
        <MainFolder @folder-main-click="showSub" />
      </div>
      <div class="col lg-4">
        <SubFolder @folder-sub-click="showFile" :folder-id="currentFolder"/>
      </div>
      <div class="col lg-4">
        <File :sub-folder-id="currentSubFolder"/>
      </div>
    </div>
  </main>
</template>

<style scoped>
  .row {
    display: flex;
  }
  .col {
    padding: 1rem;
    min-height: 100vh;
    border-right: 1px solid white;
    flex: 1 0 0%;
  }
  .col-lg-4 {
    flex: 0 0 auto;
    width: 33.33333333%;
  }
  main {
    min-width: 99vw;
    /* border: 1px solid white; */
  }
</style>
