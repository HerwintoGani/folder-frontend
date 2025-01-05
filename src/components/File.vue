<script setup lang="ts">
import { defineProps, watch } from 'vue';
import { ref, onMounted } from 'vue';

import axios from 'axios';

const props = defineProps({
  subFolderId: {
    type: Number,
    default: null,
  },
});
const fileData = ref<Array<{ file_id: number; file_name: string ; folder_sub_id: number}>>([]);

const file = async() => {
    if(props.subFolderId !== null){
        try {
            const response = await axios.post("http://localhost:3000/file/"+props.subFolderId);
            fileData.value = response.data
        } catch (error) {
            console.error("An Error Occured");
        }
    }
};

onMounted(() => {
  file();
});

watch(
  () => props.subFolderId,
  (newSubFolderId) => {
    if (newSubFolderId !== null) {
      file(newSubFolderId);
    }
  }
);
</script>

<template>
  <div v-for="f in fileData" :key="f.file_id">
    <h2>{{ f.file_name }}</h2>
  </div>
</template>

<style scoped>
</style>