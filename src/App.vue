<template>
  <div id="app">
    <div class="clock">
      <div class="clock-face">
        <div class="hand hour-hand" :style="style(hourDegrees)"></div>
        <div class="hand min-hand" :style="style(minsDegrees)"></div>
        <div class="hand sec-hand" :style="style(secondsDegrees)"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      secondsDegrees: 0,
      minsDegrees: 0,
      hourDegrees: 0
    }
  },
  methods: {
    setDate () {
      const now = new Date()
      const sec = now.getSeconds()
      this.secondsDegrees = (sec / 60) * 360 + 90
      const min = now.getMinutes()
      this.minsDegrees = (min / 60) * 360 + 90
      const hour = now.getHours()
      this.hourDegrees = 90 + (hour / 12) * 360 + (min / 12 / 60) * 360
    },
    style: function (degrees) {
      return {
        // transform: 'rotate(' + degrees + 'deg)'
        transform: `rotate(${degrees}deg)`
      }
    },
    updateDate: function () {
      this.secondsDegrees += (1 / 60) * 360
      this.minsDegrees += ((1 / 60) / 60) * 360
      this.hourDegrees += (((1 / 60) / 60) / 12) * 360
      // console.log(this.secondsDegrees)
    }
  },
  mounted: function () {
    this.setDate()
    setInterval(this.updateDate, 1000)
  }
}
</script>

<style>
html {
  background-color: #018ded;
  background-image: url(https://unsplash.it/1500/1000?image=881&blur=5);
  background-size: cover;
  font-size: 10px;
}

body {
  margin: 0;
  font-size: 2rem;
  display: flex;
  flex: 1;
  min-height: 100vh;
  align-items: center;
  justify-content: center;
}

.clock {
  width: 30rem;
  height: 30rem;
  border: 20px solid white;
  border-radius: 50%;
  margin: 50px auto;
  position: relative;
  padding: 2rem;
  box-shadow: 0 0 0 4px rgba(0, 0, 0, 0.1), inset 0 0 0 3px #efefef,
    inset 0 0 10px black, 0 0 10px rgba(0, 0, 0, 0.2);
}

.clock-face {
  position: relative;
  width: 100%;
  height: 100%;
  transform: translateY(-3px); /* 手的高度 */
}

.hand {
  width: 50%;
  height: 6px;
  background-color: #000;
  position: absolute;
  top: 50%;
  right: 50%;
  transform-origin: 100%;
  transform: rotate(90deg);
  transition: all 0.05s;
  transition-timing-function: cubic-bezier(0.1, 2.7, 0.58, 1);
}

.hour-hand {
  width: 38%;
}

.min-hand {
  height: 5.5px;
}

.sec-hand {
  height: 3px;
  background-color: #ccc;
  width: 45%;
}

.clock-face:after {
  position: absolute;
  display: block;
  width: 2rem;
  height: 2rem;
  top: 50%;
  left: 50%;
  content: "";
  background-color: #fff;
  transform: translate(-56%, -37%);
  border-radius: 50%;
  box-shadow: 0 0 0 2px rgba(0, 0, 0, 0.1), 0 0 10px rgba(0, 0, 0, 0.2);
}
</style>
