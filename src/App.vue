<template>
  <div id="app">
    <header>
      <h1>Image Uploader</h1>
      <p>Upload your images with ease!</p>
    </header>
    <main>
      <ImageUploader />
    </main>
    <footer>
      <p>© 2025 My Awesome App</p>
    </footer>
  </div>
</template>

<script>
import ImageUploader from "./components/ImageUploader.vue";

export default {
  name: "App",
  components: {
    ImageUploader,
  },
};
</script>

<style scoped>
#app {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  background: linear-gradient(to right, #ece9e6, #ffffff);
  color: #333;
  text-align: center;
  padding: 0 20px;
  box-sizing: border-box;
}

header {
  padding: 20px 0;
  background: #4a90e2;
  color: white;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

header h1 {
  margin: 0;
  font-size: 2.5em;
}

header p {
  margin: 5px 0 0;
  font-size: 1.2em;
}

main {
  flex: 1;
  display: flex;
  align-items: top;
  justify-content: top;
}

footer {
  padding: 10px 0;
  background: #4a90e2;
  color: white;
  font-size: 0.9em;
}
</style>
