<template>
  <!-- opens on spectators phone, should show something that is not sus -->
  <div class="w-screen h-screen bg-black">
    <div class="mx-auto w-2/3">
      <h1 class="text-white">Receiver</h1>
      <button class="bg-white">
        <a href="youtube://screen">Should open youtube in app</a>
      </button>
    </div>
  </div>
</template>

<script setup lang="ts">
function getMobileOperatingSystem() {
  var userAgent = navigator.userAgent || navigator.vendor;

  // Windows Phone must come first because its UA also contains "Android"
  if (/windows phone/i.test(userAgent)) {
    console.log("Windows Phone");
    return "Windows Phone";
  }

  if (/android/i.test(userAgent)) {
    console.log("Android");
    return "Android";
  }

  // iOS detection from: http://stackoverflow.com/a/9039885/177710
  if (/iPad|iPhone|iPod/.test(userAgent)) {
    console.log("iOS");
    return "iOS";
  }

  return "unknown";
}
</script>

<style scoped></style>
