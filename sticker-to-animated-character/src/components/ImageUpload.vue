<template>
  <div
    class="upload-container"
    @dragover.prevent="onDragOver"
    @dragleave.prevent="onDragLeave"
    @drop.prevent="onDrop"
    :class="{ 'drag-over': isDragging }"
  >
    <input
      type="file"
      @change="onFileSelect"
      ref="fileInput"
      style="display: none"
      accept="image/*"
    />
    <div v-if="!job_id">
      <p>Drag and drop your image here, or <a href="#" @click.prevent="openFilePicker">click to select a file</a>.</p>
    </div>
    <div v-if="job_id">
      <p>File uploaded! Job ID: {{ job_id }}</p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { uploadImage } from '../api';

const isDragging = ref(false);
const job_id = ref(null);
const fileInput = ref(null);

const onDragOver = () => {
  isDragging.value = true;
};

const onDragLeave = () => {
  isDragging.value = false;
};

const onDrop = (event) => {
  isDragging.value = false;
  const file = event.dataTransfer.files[0];
  handleFileUpload(file);
};

const onFileSelect = (event) => {
  const file = event.target.files[0];
  handleFileUpload(file);
};

const openFilePicker = () => {
  fileInput.value.click();
};

const handleFileUpload = async (file) => {
  if (!file) return;
  try {
    const response = await uploadImage(file);
    job_id.value = response.job_id;
  } catch (error) {
    console.error('Error uploading file:', error);
    // You might want to show an error message to the user
  }
};
</script>

<style scoped>
.upload-container {
  border: 2px dashed #ccc;
  border-radius: 10px;
  padding: 2rem;
  text-align: center;
  transition: background-color 0.3s, border-color 0.3s;
}

.upload-container.drag-over {
  background-color: #f0f0f0;
  border-color: #3eaf7c;
}

a {
  color: #3eaf7c;
  text-decoration: underline;
}
</style>
