<template>
    <div class="camera-modal">
        <video ref="video" class="camera-stream" id="camera"></video>
        <button disabled="disabled">hello</button>
    </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: "camera",
  components: {},
  data: {
    videoElement: HTMLVideoElement
  },
  mounted() {

    const stream = navigator.mediaDevices
      .getUserMedia({
        audio: false,
        video: { facingMode: "environment" }
      })
      .then(mediaStream => {
        let videoElement = document.querySelector("video");
        videoElement!.srcObject = mediaStream;

        videoElement!.play();

      })
      .catch(error => console.error("getUserMedia() error:", error));
  },
  methods: {
  }
});
</script>

<style scoped lang="scss">
#camera{
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  position: absolute;
  background-color: white;
  z-index: 10;
  max-height: 100%;
  object-fit: cover;
}
.camera-stream {
  width: 100%;
  max-height: 100%;
}

.button {
    
}
</style>
