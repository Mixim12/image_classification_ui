<template>
  <div class="image-uploader">
    <h1>Upload an Image for Prediction</h1>
    <form @submit.prevent="handleSubmit">
      <input type="file" @change="handleFileChange" accept="image/*" required />
      <button type="submit">Predict</button>
    </form>
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
    handleFileChange(event) {
      this.file = event.target.files[0];
    },
    async handleSubmit() {
      if (!this.file) {
        alert("Please select a file.");
        return;
      }

      const formData = new FormData();
      formData.append("file", this.file);

      try {
        const response = await axios.post(
          "http://localhost:3000/predict",
          formData,
          {
            headers: {
              "Content-Type": "multipart/form-data",
            },
          }
        );
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
  margin: 0 auto;
  text-align: center;
}
.result {
  margin-top: 20px;
}
</style>
