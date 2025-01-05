<script setup lang="ts">
import { defineProps, defineEmits, watch } from 'vue';
import { ref, onMounted } from 'vue';

import axios from 'axios';

const emit = defineEmits(['folder-sub-click']);
const props = defineProps({
  folderId: {
    type: Number,
    default: null,
  },
});
const subData = ref<Array<{ folder_sub_id: number; folder_sub_name: string ; folder_main_id: number}>>([]);

const showFile = (subFolderId: number) => {
  emit('folder-sub-click', subFolderId);
};

const folderSub = async() => {
    if(props.folderId !== null){
        try {
            const response = await axios.post("http://localhost:3000/folder_sub/"+props.folderId);
            subData.value = response.data
        } catch (error) {
            console.error("An Error Occured");
        }
    }
};

onMounted(() => {
    folderSub();
});

watch(
  () => props.folderId,
  (newFolderId) => {
    if (newFolderId !== null) {
      folderSub(newFolderId);
    }
  }
);
</script>

<template>
  <div v-for="f in subData" :key="f.folder_sub_id">
    <h2 @click="showFile(f.folder_sub_id)">{{ f.folder_sub_name }}</h2>
  </div>
</template>

<style scoped>
h2 {
  cursor: pointer;
}
h2:hover{
    background: gray;
}
</style>