<template>
  <div class="container">
    <div class="timer">
      <div class="board">
        <p>{{ formatNumber(minutes) }}:{{ formatNumber(seconds) }}:{{ formatNumber(miliseconds) }}</p>
      </div>

      <div class="actions">
        <button @click="play()" :disabled="isRunning">Play</button>
        <button @click="pause()">Pause</button>
        <button @click="reset()">Reset</button>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  
  data() {
    return {
      minutes: 0,
      seconds: 0,
      miliseconds: 0,
      isRunning: false,
      interval: null,
    }
  },

  methods: {
    formatNumber(number) {
      if (number < 10){
        return '0' + number;
      } else {
        return number;
      }
    },

    play() {
      this.isRunning = true;

      this.interval = setInterval(() => {
        this.miliseconds++;

        if (this.miliseconds === 100){
          this.miliseconds = 0;
          this.seconds++;
        }

        if (this.seconds === 60){
          this.seconds = 0;
          this.minutes++;
        }
      }, 10);
    },

    pause() {
      this.isRunning = false;
      clearInterval(this.interval);
    },

    reset() {
      this.pause();
      this.minutes = this.seconds = this.miliseconds = 0;
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
