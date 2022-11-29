<template>
  <div class="h-6 bg-white">
    <p class="text-center">↓ Scroll down to hide navbar ↓</p>
  </div>
  <div class="w-screen h-screen bg-black">
    <Spinner />
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
import NoSleep from "nosleep.js";
import Spinner from "./components/Spinner.vue";

const isMobile = "ontouchstart" in document.documentElement;
var start = 0;

var noSleep = new NoSleep();
document.addEventListener(
  "click",
  function enableNoSleep() {
    document.removeEventListener("click", enableNoSleep, false);
    noSleep.enable();
    console.log("nosleep");

    // start timer also
    start = new Date().getTime();
  },
  false
);

//view-source:https://iyt.pw/marc&youtube_web=1
function redirectYoutube(songUrl: string) {
  var time = ((new Date().getTime() - start) / 1000).toFixed();
  // var embedUrl = songUrl.replace("watch?v=", "embed/");
  // embedUrl = embedUrl + "?start=" + time + "&autoplay=1&mute=1";
  songUrl = songUrl + "?t=" + time + "s";
  console.log("redirecting to", songUrl);

  if (isMobile) {
    window.location.replace("https://www.google.com");
    window.location.href = "https://m.youtube.com";
    window.location.href = songUrl;
  } else {
    window.location.replace("https://www.google.com");
    window.location.href = "https://www.youtube.com";
    window.location.href = songUrl;
  }
}

function redirectSpotify(songUrl: string) {
  if (isMobile) {
    window.location.replace("https://www.google.com");
    window.location.href = "https://open.spotify.com";
    window.location.href = songUrl;
  } else {
    window.location.replace("https://www.google.com");
    window.location.href = "https://open.spotify.com";
    window.location.href = songUrl;
  }
}

// websocket
const ws = new WebSocket("wss://sock.agentzhao.me");

// Connection opened
ws.addEventListener("open", function (event) {
  console.log("Connected to websocket");
});

ws.addEventListener("message", (event) => {
  console.log("Server:", event.data);
  try {
    const data = JSON.parse(event.data);
    // if (data.id == id) return;
    if (data.platform == "youtube") {
      redirectYoutube(data.songUrl);
    } else if (data.platform == "spotify") {
      redirectSpotify(data.songUrl);
    }
  } catch (e) {
    //nothing
  }
});
</script>

<style scoped></style>
