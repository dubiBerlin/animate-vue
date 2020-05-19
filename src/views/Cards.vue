<template>
  <transition-group
    appear
    @before-enter="beforeEnter"
    @enter="enter"
    :css="false"
  >
    <div class="card" v-for="card in cards" :key="card.id">
      <p>{{ card.title }}</p>
    </div>
  </transition-group>
</template>

<script>
import Velocity from "velocity-animate"

export default {
  data() {
    return {
      cards: [
        { title: "Could contain anything", id: 123 },
        { title: "Endless possibilities", id: 456 },
        { title: "wwwww", id: 455 },
        { title: "Endless possibilities", id: 453 },
        { title: "Endless possibilities", id: 457 },
        { title: "Endless possibilities", id: 451 },
        { title: "Endless possibilities", id: 454 }
      ]
    }
  },
  methods: {
    beforeEnter(el) {
      el.style.opacity = 0
      el.style.width = "0em"
    },
    enter(el, done) {
      Velocity(
        el,
        { opacity: 1, width: "12em", rotateZ: "13deg" },
        { duration: 1000, easing: [300, 80], complete: done }
      )
    }
  }
}
</script>

<style scoped>
.card {
  height: 4em;
  width: 12em;
  border-radius: 1%;
  background-color: #e0e0e0;
  box-shadow: 0.08em 0.03em 0.4em #ababab;
  padding-top: 1em;
}
</style>