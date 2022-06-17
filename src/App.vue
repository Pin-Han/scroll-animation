<script setup>
import { computed, onMounted, ref } from "vue";

const progress = ref(0);
onMounted(() => {
  const app = document.querySelector("#app");

  app.addEventListener("scroll", () => {
    if (app.scrollTop < window.innerHeight) {
      progress.value = 3;
    } else if (app.scrollTop > window.innerHeight * 2) {
      progress.value = 1;
    } else {
      //progress
      progress.value =
        3 - 2 * ((app.scrollTop - window.innerHeight) / window.innerHeight);
    }
  });
});
const fixClass = computed(() => {
  return progress.value > 1;
});
</script>

<template>
  <div class="section text">
    Lorem ipsum dolor sit amet consectetur adipisicing elit.
  </div>
  <div
    class="section"
    id="section2"
    :style="{ '--scale': progress }"
    :class="{ sticky: fixClass }"
  >
    <div class="phone">
      <img src="https://picsum.photos/seed/picsum/1920/1200" alt="" />
      <div class="rect"></div>
    </div>
  </div>
  <div class="section" id="section3" :class="{ static: fixClass }">
    <div class="phone">
      <img src="https://picsum.photos/seed/picsum/1920/1200" alt="" />
      <div class="rect"></div>
    </div>
  </div>
  <div class="section text">
    Lorem ipsum dolor sit amet consectetur adipisicing elit.
  </div>
</template>

<style>
* {
  margin: 0;
  padding: 0;
}
#app {
  width: 100vw;
  height: 100vh;
  overflow: auto;
}
.section {
  position: relative;
  width: 100%;
  height: 100vh;
  background-color: white;
  overflow: hidden;
}
.text {
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 100px;
  text-align: center;
}
#section2,
#section3 {
  background-color: black;
}
#section2 {
  --scale: 3;
}
#section3 {
  --scale: 1;
}
.sticky {
  position: sticky !important;
  top: 0;
  left: 0;
}

.static {
  position: static !important;
}
.phone {
  position: absolute;
  width: 100%;
  height: 100%;
  transform: scale(var(--scale));
}

.phone > * {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.phone > img {
  clip-path: inset(15% 7% round 5%);
  width: 60%;
  height: auto;
}

.phone > .rect {
  width: 50%;
  height: 0;
  padding-top: 25%;
  border: 10px solid white;
  border-radius: 10px;
}
@media (max-width: 600px) {
  .text {
    font-size: 20px;
  }
  .phone > .rect {
    border: 3px solid white;
  }
}
</style>
