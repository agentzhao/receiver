<template>
  <div class="w-screen h-screen bg-black" @click="timer">
    <img
      src="https://user-images.githubusercontent.com/20024592/194550744-14659755-95ad-4bb0-bda8-d26c6c668ae4.png"
      class="w-screen"
      @click="timer"
      id="youtube"
    />
    <input
      type="text"
      class="absolute inset-x-0 top-2 ml-12 w-8/12 h-6 bg-transparent outline-none"
      id="input"
    />
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

    document.querySelector("input")!.focus();
    // change image source
    document.querySelector("img")!.src =
      "https://user-images.githubusercontent.com/20024592/194550994-14b5c0f6-eafa-4a01-a4ab-9cbd0b9e887b.png";
  },
  false
);

//view-source:https://iyt.pw/marc&youtube_web=1
function redirectYoutube(songUrl: string) {
  var time = ((new Date().getTime() - start) / 1000).toFixed();
  // var embedUrl = songUrl.replace("watch?v=", "embed/");
  // embedUrl = embedUrl + "?start=" + time + "&autoplay=1&mute=1";
  songUrl = songUrl + "&t=" + time + "s";
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
