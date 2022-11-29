<template>
  <div class="text-black ytp-spinner">
    <div class="ytp-spinner-container">
      <div class="ytp-spinner-rotator">
        <div class="ytp-spinner-left">
          <div class="ytp-spinner-circle"></div>
        </div>
        <div class="ytp-spinner-right">
          <div class="ytp-spinner-circle"></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts"></script>

<style scoped>
.ytp-spinner {
  position: absolute;
  left: 50%;
  top: 50%;
  width: 64px;
  margin-left: -32px;
  z-index: 18;
  pointer-events: none;
}

.ytp-spinner-container {
  pointer-events: none;
  position: absolute;
  width: 100%;
  padding-bottom: 100%;
  top: 50%;
  left: 50%;
  margin-top: -50%;
  margin-left: -50%;
  animation: ytp-spinner-linspin 1568.2352941176ms linear infinite;
}

@keyframes ytp-spinner-linspin {
  to {
    transform: rotate(360deg);
  }
}

.ytp-spinner-rotator {
  position: absolute;
  width: 100%;
  height: 100%;
  animation: ytp-spinner-easespin 5332ms cubic-bezier(0.4, 0, 0.2, 1) infinite
    both;
}

@keyframes ytp-spinner-easespin {
  12.5% {
    transform: rotate(135deg);
  }
  25% {
    transform: rotate(270deg);
  }
  37.5% {
    transform: rotate(405deg);
  }
  50% {
    transform: rotate(540deg);
  }
  62.5% {
    transform: rotate(675deg);
  }
  75% {
    transform: rotate(810deg);
  }
  87.5% {
    transform: rotate(945deg);
  }
  to {
    transform: rotate(1080deg);
  }
}

.ytp-spinner-circle {
  -moz-box-sizing: border-box;
  box-sizing: border-box;
  position: absolute;
  width: 200%;
  height: 100%;
  border-style: solid;
  border-color: #ddd #ddd transparent;
  border-radius: 50%;
  border-width: 6px;
}

.ytp-spinner-left {
  position: absolute;
  top: 0;
  left: 0;
  right: 49%;
  bottom: 0;
  overflow: hidden;
}

.ytp-spinner-left .ytp-spinner-circle {
  left: 0;
  right: -100%;
  border-right-color: transparent;
  animation: ytp-spinner-left-spin 1333ms cubic-bezier(0.4, 0, 0.2, 1) infinite
    both;
}

@keyframes ytp-spinner-left-spin {
  0% {
    -webkit-transform: rotate(130deg);
    transform: rotate(130deg);
  }
  50% {
    -webkit-transform: rotate(-5deg);
    transform: rotate(-5deg);
  }
  to {
    -webkit-transform: rotate(130deg);
    transform: rotate(130deg);
  }
}

.ytp-spinner-right {
  position: absolute;
  top: 0;
  left: 49%;
  right: 0;
  bottom: 0;
  overflow: hidden;
}

.ytp-spinner-right .ytp-spinner-circle {
  left: -100%;
  right: 0;
  border-left-color: transparent;
  animation: ytp-right-spin 1333ms cubic-bezier(0.4, 0, 0.2, 1) infinite both;
}

@keyframes ytp-right-spin {
  0% {
    -webkit-transform: rotate(-130deg);
    transform: rotate(-130deg);
  }
  50% {
    -webkit-transform: rotate(5deg);
    transform: rotate(5deg);
  }
  to {
    -webkit-transform: rotate(-130deg);
    transform: rotate(-130deg);
  }
}
</style>
