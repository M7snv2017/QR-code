<script setup>
  import {ref}from 'vue'
  let text=ref('')
  let img=document.getElementsByTagName("img")
  const genQR = () => {
  if (text.value.trim() !== '') {
    let qrUrl = "https://api.qrserver.com/v1/create-qr-code/?data=" + encodeURIComponent(text.value) + "&size=150x150&color=DAA520&bgcolor=000000&format=png&margin=10"; // Blue QR

    img[0].src = qrUrl;
    
  }
}
</script>
<template>
  <div class="container">
    <h1>Golden QR code Generator</h1>
    <input type="text" v-model="text" placeholder="Enter your texty">
    <button @click="genQR">Get QR</button>
    <img id="img" />
  </div>
</template>

<style>
button{
  
}
input{

}
h1{
  color: #DAA520;
}
body{
  background-color: #404040;
}
.container {
  width: 50%; 
  margin: 0 auto;
  text-align: center; 
  display: block;
}
img{
  margin: 0 auto;
  text-align: center; 
  display: block;
}

</style>