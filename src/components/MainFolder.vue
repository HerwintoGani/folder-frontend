<script setup lang="ts">
import { defineProps, defineEmits } from 'vue';
import { ref, onMounted } from 'vue';

import axios from 'axios';

const emit = defineEmits(['folder-main-click']);
const folderData = ref<Array<{ folder_main_id: number; folder_main_name: string }>>([]);

const showSub = (folderId: number) => {
  emit('folder-main-click', folderId);
};

const folderMain = async() => {
    try {
        const response = await axios.post("http://localhost:3000/folder_main");
        folderData.value = response.data
    } catch (error) {
        console.error("An Error Occured");
    }
};

onMounted(() => {
    folderMain();
});
</script>

<template>
    <div v-for="f in folderData" :key="f.folder_main_id" class="folder-main">
        <h2 @click="showSub(f.folder_main_id)">{{ f.folder_main_name }}</h2>
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