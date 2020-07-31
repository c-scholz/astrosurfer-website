<template>
  <div class="section-wrap">
    <StartSection></StartSection>
    <PlanetSection></PlanetSection>
    <PlanetSection></PlanetSection>
    <PlanetSection></PlanetSection>
  </div>
</template>

<script>
import StartSection from './components/StartSection.vue'
import PlanetSection from './components/PlanetSection.vue'
import { onMounted, onUnmounted } from 'vue'

export default {
  name: 'App',
  components: {
    StartSection,
    PlanetSection
  },
  setup() {
    var fadeInElements = []

    const handleScroll = () => {
      for (var i = 0; i < fadeInElements.length; i++) {
        console.log(fadeInElements)
        var elem = fadeInElements[i]
        if (isElemVisible(elem)) {
          elem.style.opacity = '1'
        } else {
          elem.style.opacity = '0'
        }
      }
    }

    const isElemVisible = (el) => {
      var rect = el.getBoundingClientRect()
      var elemTop = rect.top + 500 // 200 = buffer
      var elemBottom = rect.bottom
      return elemTop < window.innerHeight && elemBottom >= 0
    }

    onMounted(() => {
      fadeInElements = Array.from(document.getElementsByClassName('content'))
      document.getElementById("app").addEventListener("scroll", handleScroll)
      handleScroll()
    })
    onUnmounted(() => {
      document.getElementById("app").removeEventListener('scroll', handleScroll)
    })
  }
}
</script>

<style>
body {
  margin: 0;
}
#app {
  width: 100%;
  height: 100vh;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  overflow-y: scroll;
  scroll-snap-type: y mandatory;
  scroll-snap-stop: always;
}
section {
  width: 100%;
  min-width: 360px;
  height: 100vh;
  display: flex;
  flex-flow: column wrap;
  justify-content: center;
  scroll-snap-align: start;
  background-color: rgba(25, 25, 35, 1);
}

.content {
  color: white;
  text-shadow: .1em .1em black;
  margin: 0% 15%;
  opacity: 0;
  transition: 0.3s all ease-out;
}
</style>
