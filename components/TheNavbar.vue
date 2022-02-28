<template>
  <nav>
    <div class="flex navbar">
      <img src="logo.svg" alt="" />
      <img
        src="icon-hamburger.svg"
        v-if="!active"
        alt=""
        @click="toggleSlider"
      />
    </div>

    <div class="slider flex" :class="{ active: active }">
      <img
        src="icon-close.svg"
        alt=""
        style="align-self: flex-end"
        @click="toggleSlider"
      />
      <span @click="toggleSlider"
        ><nuxt-link :to="{ name: 'index' }">Home</nuxt-link></span
      >
      <span @click="toggleSlider">
        <nuxt-link @click="toggleSlider" :to="{ name: 'destination' }"
          >Destination</nuxt-link
        ></span
      >
      <span @click="toggleSlider">
        <nuxt-link @click="toggleSlider" :to="{ name: 'crew' }"
          >Crew</nuxt-link
        ></span
      >
      <span @click="toggleSlider">
        <nuxt-link @click="toggleSlider" :to="{ name: 'technology' }"
          >Technology</nuxt-link
        ></span
      >
    </div>
  </nav>
</template>

<script>
export default {
  data() {
    return {
      active: false,
    }
  },
  methods: {
    toggleSlider() {
      this.active = !this.active
    },
  },
}
</script>

<style scoped>
.navbar {
  justify-content: space-between;
  align-items: center;
  padding: 1rem;
}
.slider {
  position: absolute;
  right: -250px;
  top: 0;
  flex-direction: column;
  width: 250px;
  padding: 2rem 1.5rem;
  z-index: 1;
  background-color: #ffffff;
  height: 100vh;
  background: hsl(0, 50%, 100%, 0.1);
  backdrop-filter: blur(4px);
}

.active {
  animation-name: slide;
  animation-duration: 1s;
  animation-fill-mode: forwards;
}

/* .slide-enter-active {
  animation-name: slide;
  animation-duration: 0.5s;
  animation-fill-mode: forwards;
}

.slide-leave-active {
  animation: slide 0.5s reverse;
} */

@keyframes slide {
  0% {
    right: -250px;
  }

  100% {
    right: 0px;
  }
}
</style>
