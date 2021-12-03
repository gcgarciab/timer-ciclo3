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
body {
  margin: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.container {
  height: 100vh;
  background-color: #018C8C;
  display: flex;
	flex-direction: row;
	flex-wrap: nowrap;
	justify-content: center;
	align-items: center;
  align-content: center;
}

.timer {
  background-color: #fff;
  padding: 10% 15%;
  width: 80%;
  height: 80vh;
  box-sizing: border-box;
  border: 2px solid #000;
  display: flex;
	flex-direction: column;
	flex-wrap: nowrap;
	justify-content: center;
	align-items: stretch;
	align-content: center;
}

.board {
  background-color: #4D4C4C;
  color: #fff;
  height: 60%;
  display: flex;
	flex-direction: row;
	flex-wrap: nowrap;
	justify-content: center;
	align-items: center;
  align-content: center;
  border: 2px solid #000;
}

p {
  margin: 0;
  font-size: 60px;
}

.actions {
  background-color: #DB143C;
  padding: 40px;
  display: flex;
	flex-direction: row;
	flex-wrap: nowrap;
	justify-content: space-between;
	align-items: center;
	align-content: center;
  border: 2px solid #000;
  border-top: 0;
}

.actions button {
  border-radius: none;
  border: 2px solid #000;
  font-size: 20px;
  font-weight: bold;
  padding: 8px 15px;
  color: #000;
  cursor: pointer;
}

button:disabled {
  cursor: no-drop;
}
</style>
