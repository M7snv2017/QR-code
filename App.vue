<script setup>
  import { ref } from 'vue';

  let text = ref('');
  let img = ref(null);

  const genQR = () => {
    if (text.value.trim() !== '') {
      let qrUrl = "https://api.qrserver.com/v1/create-qr-code/?" +
                  "data=" + encodeURIComponent(text.value) +
                  "&size=200x200" +
                  "&color=DAA520" +  // Gold
                  "&bgcolor=404040" +  // Dark Gray
                  "&format=png" +
                  "&margin=10";

      if (img.value) img.value.src = qrUrl;
    }
  };
</script>

<template>
  <div class="container">
    <h1>Golden QR Code Generator</h1>
    <input type="text" v-model="text" placeholder="Enter your text">
    <button @click="genQR">Generate QR</button>
    <img ref="img" />
  </div>
</template>

<style>
/* Apply styles to the entire page */
body {
  background-color: #404040; /* Dark gray */
  font-family: Arial, sans-serif;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  margin: 0;
}

/* Center container */
.container {
  width: 40%;
  text-align: center;
  background: rgba(255, 255, 255, 0.1);
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.5);
}

/* Style the heading */
h1 {
  color: #DAA520; /* Gold */
  font-size: 28px;
  margin-bottom: 20px;
  text-transform: uppercase;
}

/* Style the input field */
input {
  width: 80%;
  padding: 10px;
  font-size: 16px;
  border: 2px solid #DAA520;
  border-radius: 5px;
  background: #303030;
  color: white;
  outline: none;
  margin-bottom: 15px;
}

/* Style the button */
button {
  background-color: #DAA520;
  color: #404040;
  font-size: 18px;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: 0.3s;
}

button:hover {
  background-color: #B8860B; /* Darker Gold */
}

/* Center the image */
img {
  display: block;
  margin: 20px auto 0;
  max-width: 200px;
  border-radius: 10px;
}
</style>
