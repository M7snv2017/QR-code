<script setup>
  import { ref } from 'vue';

  let text = ref('');
  let qrUrl = ref(''); // Store QR URL

  const genQR = () => {
    if (text.value.trim() !== '') {
      qrUrl.value = "https://api.qrserver.com/v1/create-qr-code/?" +
                  "data=" + encodeURIComponent(text.value) +
                  "&size=200x200" +
                  "&color=B8860B" +  // Gold
                  "&bgcolor=404040" +  // Dark Gray
                  "&format=png" +
                  "&margin=10";
    }
  };

  const downloadQR = async () => {
    if (!qrUrl.value) return;

    try {
      const response = await fetch(qrUrl.value);
      const blob = await response.blob();
      const blobUrl = URL.createObjectURL(blob);

      const link = document.createElement("a");
      link.href = blobUrl;
      link.download = "QR_Code.png";
      document.body.appendChild(link);
      link.click();
      document.body.removeChild(link);

      // Cleanup blob URL
      URL.revokeObjectURL(blobUrl);
    } catch (error) {
      console.error("Failed to download QR code:", error);
    }
  };
</script>

<template>
  <div class="container">
    <h1>Golden QR Code Generator</h1>
    <input type="text" v-model="text" placeholder="Enter Your Link">
    <button @click="genQR">Generate QR</button>
    
    <!-- QR Image -->
    <img v-if="qrUrl" :src="qrUrl" alt="QR Code" />

    <!-- Download Button (Shows Only When QR is Generated) -->
    <button v-if="qrUrl" @click="downloadQR" class="download-btn">Download QR</button>
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
  width: 100%;
  text-align: center;
  background: rgba(0, 0, 0, 0.1);
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.5);
}

/* Style the heading */
h1 {
  color: #B8860B; /* Gold */
  font-size: 24px;
  margin-bottom: 20px;
}

/* Style the input field */
input {
  width: 80%;
  padding: 10px;
  font-size: 16px;
  border: 2px solid #B8860B;
  border-radius: 5px;
  background: #303030;
  color: white;
  outline: none;
  margin-bottom: 15px;
}

/* Style buttons */
button {
  background-color: #B8860B;
  color: #404040;
  font-size: 18px;
  padding: 10px 20px;
  border: none;
  border-radius: 10px;
  cursor: pointer;
  transition: 0.3s;
  width: 80%;
  margin-top: 10px;
}

button:hover {
  background-color: #A07000; /* Darker Gold */
}

/* Style the download button */
.download-btn {
  color: #202020;
  width: 40%;
  font-size: medium;
  font-weight: bold;
}

.download-btn:hover {
  background-color: #E6C200; /* Slightly darker gold */
}

/* Center the image */
img {
  display: block;
  margin: 20px auto 0;
  max-width: 200px;
  border-radius: 10px;
}
</style>