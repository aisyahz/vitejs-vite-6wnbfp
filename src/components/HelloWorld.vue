<!-- HelloWorld.vue -->
<template>
  <div>
    <!-- ... (existing template code) ... -->
    <QrScanner v-on:qr-detected="handleQrDetected" />
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import Quagga from 'quagga';

const scannedQrCode = ref('');

onMounted(() => {
  Quagga.init(
    {
      // ... (QR code scanning initialization)
    },
    (err) => {
      // ... (QR code scanning error handling)
    }
  );

  Quagga.onDetected((result) => {
    const code = result.codeResult.code;
    handleQrDetected(code);
    Quagga.stop();
  });
});

const handleQrDetected = (code) => {
  scannedQrCode.value = code;
};
</script>
