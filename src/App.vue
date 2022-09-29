<template>
  <div class="w-screen h-screen bg-black">
    <div class="flex flex-col justify-center items-center mx-auto w-2/3">
      <h1 class="my-10 text-3xl text-white">Receiver</h1>
      <h3 class="mb-10 text-xl text-white">ID: {{ id }}</h3>
      <button class="mb-10 w-20 h-10 bg-orange-400" @click="timer">
        start
      </button>
      <button class="bg-red-400" @click="redirecttest">redirecttest</button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
import NoSleep from "nosleep.js";

const isMobile = "ontouchstart" in document.documentElement;

var noSleep = new NoSleep();
// Enable wake lock.
// (must be wrapped in a user input event handler e.g. a mouse or touch handler)
document.addEventListener(
  "click",
  function enableNoSleep() {
    document.removeEventListener("click", enableNoSleep, false);
    noSleep.enable();
    console.log("nosleep");
  },
  false
);

//view-source:https://iyt.pw/marc&youtube_web=1
function redirectYoutube(songUrl: string) {
  var time = ((new Date().getTime() - start) / 1000).toFixed();
  var embedUrl = songUrl.replace("watch?v=", "embed/");
  embedUrl = embedUrl + "?start=" + time + "&autoplay=1&mute=1";
  console.log("redirecting to", embedUrl);

  if (isMobile) {
    window.location.replace("https://www.google.com");
    window.location.assign("https://m.youtube.com");
    window.location.assign(embedUrl.replace("://www", "://m"));
  } else {
    window.location.replace("https://www.google.com");
    window.location.assign("https://www.youtube.com");
    window.location.assign(embedUrl);
  }
}

function redirectSpotify(songUrl: string) {
  if (isMobile) {
    window.location.replace("https://www.google.com");
    window.location.assign("https://open.spotify.com");
    window.location.assign(songUrl);
  } else {
    window.location.replace("https://www.google.com");
    window.location.assign("https://open.spotify.com");
    window.location.assign(songUrl);
  }
}

function redirecttest() {
  window.location.replace("https://www.google.com");
  window.location.replace("https://www.youtube.com");
  window.location.replace(
    "https://www.youtube.com/embed/75-Com9Bo_s?start=30&autoplay=1&mute=1"
  );
}

var id = 0;
id = Math.floor(Math.random() * 1000 + 1);

var start = 0;
function timer() {
  start = new Date().getTime();
}

// websocket
const ws = new WebSocket("wss://sock.agentzhao.me");

// Connection opened
ws.addEventListener("open", function (event) {
  console.log("Connected with id: " + id);
  ws.send("receiver " + id);
});

ws.addEventListener("message", (event) => {
  console.log("Server:", event.data);
  try {
    const data = JSON.parse(event.data);
    if (data.id == id && data.platform == "youtube") {
      redirectYoutube(data.songUrl);
    } else if (data.id == id && data.platform == "spotify") {
      redirectSpotify(data.songUrl);
    }
  } catch (e) {
    //nothing
  }
});
</script>

<style scoped></style>
