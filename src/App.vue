<script setup>
import { Html5QrcodeScanner } from 'html5-qrcode'
import { onBeforeUnmount, onMounted, ref } from 'vue';

const scanner = ref(null)
const scannedData = ref(null)

function onScanSuccess(decodedText) {
  scannedData.value = decodedText;
}

onMounted(() => {
  scanner.value = new Html5QrcodeScanner("reader", { fps: 10, qrbos: 250 });
  scanner.value.render(onScanSuccess)
});

onBeforeUnmount(() => {
  if (scanner.value) {
    scanner.value.clear();
  }
})

</script>

<template>
  <div class="container d-flex p-5">
    <div>
      <h1>Silahkan Tapping Kartu Siswa Anda</h1>
      <div class="section">
        <div id="reader"></div>
        <p v-if="scannedData">Scanned data: {{ scannedData }}</p>
      </div>
    </div>

    <section class="ml-5">
      <table class="table table-strip table-border table-sm">
        <thead>
          <tr>
            <td>No</td>
            <td>Nama</td>
            <td>Kelas</td>
            <td>Attend</td>
            <td>Time</td>
          </tr>
        </thead>

        <tbody>
          <tr>
            <td>1 .</td>
            <td>Fajri Muhammad Tio</td>
            <td>VII A</td>
            <td>Hadir</td>
            <td>121212121</td>
          </tr>
        </tbody>
      </table>
    </section>
  </div>
</template>
