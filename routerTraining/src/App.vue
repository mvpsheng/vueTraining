<template>
  <div>
    <div v-if="countdownState === 'setting'">
      <h1>设置倒计时时间</h1>
      <label for="countdown-input">倒计时时间（1-10秒）：</label>
      <input type="number" id="countdown-input" v-model="countdownSeconds" min="1" max="10">
      <button @click="startCountdown">确定</button>
    </div>
    <div v-else-if="countdownState === 'running'">
      <h1>倒计时进行中</h1>
      <p>{{ countdownSeconds }} 秒</p>
    </div>
    <div v-else>
      <h1>倒计时结束</h1>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      countdownSeconds: 0,
      countdownState: 'setting'
    };
  },
  methods: {
    startCountdown() {
      this.countdownState = 'running';
      let countdownInterval = setInterval(() => {
        this.countdownSeconds--;
        if (this.countdownSeconds <= 0) {
          clearInterval(countdownInterval);
          this.countdownState = 'finished';
        }
      }, 1000);
    }
  }
};
</script>
