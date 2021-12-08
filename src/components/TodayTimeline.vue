<template>
  <div class="main-container">
    <div class="row align-items-center ">
      <div class="col-md-4 yellow bold">{{ title }}</div>
      <div class="col-md-4 red text-center">{{ time }}</div>
      <div class="col-md-4 text-right pr-2">
        <div
          class="btn-group btn-group-sm yellow"
          role="group"
          aria-label="Basic mixed styles example"
        >
          <button
            type="button"
            class="btn btn-outline-warning"
            @click="start"
            v-if="!running"
          >
            Start
          </button>
          <button
            type="button"
            class="btn btn-outline-danger"
            @click="stop"
            v-else
          >
            Stop
          </button>
          <button type="button" class="btn btn-outline-warning" @click="reset">
            Reset
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "Timer",
  props: ["title", "index"],
  data: () => ({
    time: "00:00:00.000",
    timeBegan: null,
    timeStopped: null,
    stoppedDuration: 0,
    started: null,
    running: false,
  }),
  methods: {
    // start timer
    start() {
      this.$emit("currentlyStart", this.index);
      if (this.running) return;
      if (this.timeBegan === null) {
        this.reset();
        this.timeBegan = new Date();
      }
      if (this.timeStopped !== null) {
        this.stoppedDuration += new Date() - this.timeStopped;
      }

      this.started = setInterval(this.clockRunning, 10);
      this.running = true;
    },
    // reset timer function
    reset() {
      this.running = false;
      clearInterval(this.started);
      this.stoppedDuration = 0;
      this.timeBegan = null;
      this.timeStopped = null;
      this.time = "00:00:00.000";
    },
    // stop timer function
    stop() {
      this.running = false;
      this.timeStopped = new Date();
      clearInterval(this.started);
      this.$emit("stopTime", this.title, this.time, this.running);
    },
    save() {
      console.log("time saved", this.time);
    },
    clockRunning() {
      var currentTime = new Date(),
        timeElapsed = new Date(
          currentTime - this.timeBegan - this.stoppedDuration
        ),
        hour = timeElapsed.getUTCHours(),
        min = timeElapsed.getUTCMinutes(),
        sec = timeElapsed.getUTCSeconds(),
        ms = timeElapsed.getUTCMilliseconds();

      this.time =
        this.zeroPrefix(hour, 2) +
        ":" +
        this.zeroPrefix(min, 2) +
        ":" +
        this.zeroPrefix(sec, 2) +
        "." +
        this.zeroPrefix(ms, 3);
    },
    zeroPrefix(num, digit) {
      var zero = "";
      for (var i = 0; i < digit; i++) {
        zero += "0";
      }
      return (zero + num).slice(-digit);
    },
  },
};
</script>
