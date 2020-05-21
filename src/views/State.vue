<template>
  <div>
    <div :style="{ width: tweenedNumber + 'px'}" class="bar">
      <span>{{ tweenedNumber.toFixed(0) }}</span>
    </div>
  </div>
</template>

<script>
import gsap from "gsap"

export default {
  data() {
    return {
      number: 0,
      tweenedNumber: 0
    }
  },
  methods: {
    randomNumber() {
      this.number = Math.floor(Math.random() * (800 - 0))
    }
  },
  watch: {
    number(newValue) {
      gsap.to(this.$data, {
        duration: 1,
        ease: "circ.out",
        tweenedNumber: newValue
      })
    }
  },
  created() {
    setInterval(this.randomNumber, 1500)
  }
}
</script>

<style scoped>
.bar {
  height: 3.5em;
  width: 3.5em;
  border-radius: 1%;
  background-color: #16c0b0;
  box-shadow: 0.08em 0.03em 0.4em #ababab;
}

.bar > span {
  line-height: 3.5em;
  vertical-align: middle;
}
</style>
