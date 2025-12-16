<script setup>
import { ref } from 'vue'
import QRCode from 'qrcode'

const url = ref('')
const qrCodeDataUrl = ref('')
const errorMessage = ref('')

const generateQRCode = async () => {
  // Validate input
  if (!url.value.trim()) {
    errorMessage.value = 'Please enter a URL'
    qrCodeDataUrl.value = ''
    return
  }

  try {
    // Clear error message
    errorMessage.value = ''

    // Generate QR code as data URL
    const dataUrl = await QRCode.toDataURL(url.value, {
      width: 256,
      margin: 2,
      color: {
        dark: '#000000',
        light: '#ffffff'
      }
    })

    qrCodeDataUrl.value = dataUrl
  } catch (err) {
    errorMessage.value = 'Failed to generate QR code'
    console.error(err)
  }
}

const downloadQRCode = () => {
  if (!qrCodeDataUrl.value) return

  // Create download link
  const link = document.createElement('a')
  link.href = qrCodeDataUrl.value
  link.download = 'qrcode.png'
  document.body.appendChild(link)
  link.click()
  document.body.removeChild(link)
}

// Allow Enter key to generate QR code
const handleKeyPress = (event) => {
  if (event.key === 'Enter') {
    generateQRCode()
  }
}
</script>

<template>
  <div class="container">
    <h1>QR Code Generator</h1>

    <div class="input-group">
      <label for="url-input">Enter URL:</label>
      <input
        id="url-input"
        v-model="url"
        type="url"
        placeholder="https://example.com"
        @keypress="handleKeyPress"
      >
      <div v-if="errorMessage" class="error-message">
        {{ errorMessage }}
      </div>
    </div>

    <button class="generate-btn" @click="generateQRCode">
      Generate QR Code
    </button>

    <div class="qrcode-container">
      <div v-if="!qrCodeDataUrl" class="placeholder-text">
        Your QR code will appear here
      </div>
      <img v-else :src="qrCodeDataUrl" alt="QR Code" class="qrcode-image">
    </div>

    <button
      v-if="qrCodeDataUrl"
      class="download-btn"
      @click="downloadQRCode"
    >
      Download PNG
    </button>
  </div>
</template>

<style scoped>
.container {
  background: white;
  border-radius: 20px;
  padding: 40px;
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
  max-width: 500px;
  width: 100%;
}

h1 {
  text-align: center;
  color: #333;
  margin-bottom: 30px;
  font-size: 28px;
}

.input-group {
  margin-bottom: 20px;
}

label {
  display: block;
  margin-bottom: 8px;
  color: #555;
  font-weight: 500;
}

input[type="text"] {
  width: 100%;
  padding: 12px 16px;
  border: 2px solid #e0e0e0;
  border-radius: 8px;
  font-size: 16px;
  transition: border-color 0.3s;
}

input[type="text"]:focus {
  outline: none;
  border-color: #667eea;
}

button {
  width: 100%;
  padding: 14px;
  color: white;
  border: none;
  border-radius: 8px;
  font-size: 16px;
  font-weight: 600;
  cursor: pointer;
  transition: transform 0.2s, box-shadow 0.2s;
}

button:hover {
  transform: translateY(-2px);
}

button:active {
  transform: translateY(0);
}

.generate-btn {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
}

.generate-btn:hover {
  box-shadow: 0 4px 12px rgba(102, 126, 234, 0.4);
}

.qrcode-container {
  margin: 30px 0;
  text-align: center;
  min-height: 256px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.qrcode-image {
  max-width: 100%;
  height: auto;
}

.download-btn {
  background: linear-gradient(135deg, #11998e 0%, #38ef7d 100%);
  margin-top: 20px;
}

.download-btn:hover {
  box-shadow: 0 4px 12px rgba(17, 153, 142, 0.4);
}

.error-message {
  color: #e74c3c;
  font-size: 14px;
  margin-top: 8px;
}

.placeholder-text {
  color: #999;
  font-size: 14px;
}
</style>
