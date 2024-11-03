<template>
  <div class="image-uploader">
    <h1>Upload an Image for Prediction</h1>
    <div class="upload-area" @dragover.prevent @dragenter.prevent @drop.prevent="handleDrop" @click="triggerFileSelect">
      <p v-if="!file">Drag & Drop your image here or click to select</p>
      <p v-else>{{ file.name }}</p>
    </div>
    <input type="file" ref="fileInput" @change="handleFileChange" accept="image/*" style="display: none" />
    <button :disabled="!file" @click="handleSubmit">Predict</button>
    <div v-if="prediction" class="result">
      <h2>Prediction Result:</h2>
      <p>{{ prediction }}</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "ImageUploader",
  data() {
    return {
      file: null,
      prediction: null,
    };
  },
  methods: {
    triggerFileSelect() {
      this.$refs.fileInput.click();
    },
    handleFileChange(event) {
      this.file = event.target.files[0];
    },
    handleDrop(event) {
      const droppedFiles = event.dataTransfer.files;
      if (droppedFiles.length) {
        this.file = droppedFiles[0];
      }
    },
    async handleSubmit() {
      if (!this.file) {
        alert("Please select a file.");
        return;
      }

      const formData = new FormData();
      formData.append("file", this.file);

      try {
        const response = await axios.post("http://localhost:3000/predict", formData, {
          headers: {
            "Content-Type": "multipart/form-data",
          },
        });
        this.prediction = response.data.prediction;
      } catch (error) {
        console.error("Error during prediction:", error);
        alert("An error occurred during prediction.");
      }
    },
  },
};
</script>

<style scoped>
.image-uploader {
  max-width: 600px;
  margin: 50px auto;
  text-align: center;
  font-family: Arial, sans-serif;
}

h1 {
  margin-bottom: 20px;
}

.upload-area {
  border: 2px dashed #ccc;
  padding: 40px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.upload-area:hover {
  background-color: #f9f9f9;
}

.upload-area p {
  margin: 0;
  color: #999;
}

button {
  margin-top: 20px;
  padding: 10px 20px;
  background-color: #007bff;
  color: white;
  border: none;
  cursor: pointer;
  border-radius: 4px;
}

button:disabled {
  background-color: #ccc;
  cursor: not-allowed;
}

.result {
  margin-top: 30px;
}

.result h2 {
  margin-bottom: 10px;
}
</style>
