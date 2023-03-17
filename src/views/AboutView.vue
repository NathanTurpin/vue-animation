<template>
  <div class="about">
    <transition-group
      tag="ul"
      @before-enter="beforeEnter"
      @enter="enter"
      class="card"
      appear
    >
      <li
        class="card__list"
        v-for="(icon, index) in icons"
        :key="icon.name"
        :data-index="index"
      >
        <span class="material-symbols-outlined">{{ icon.name }}</span>
        <div class="card__text">{{ icon.text }}</div>
      </li>
    </transition-group>
  </div>
</template>

<script>
import { ref } from "vue";
import gsap from "gsap";
export default {
  setup() {
    const icons = ref([
      { name: "alternate_email", text: "by email" },
      { name: "local_phone", text: "by phone" },
      { name: "local_post_office", text: "by post" },
      { name: "local_fire_department", text: "by smoke signal" },
    ]);

    const beforeEnter = (el) => {
      console.log(el);
      el.style.opacity = "0";
      el.style.transform = "translateY(100px)";
    };

    const enter = (el, done) => {
      gsap.to(el, {
        opacity: 1,
        y: 0,
        duration: 0.8,
        onComplete: done,
        delay: el.dataset.index * 0.2,
      });
    };
    return { icons, beforeEnter, enter };
  },
};
</script>
<style lang="scss">
.card {
  padding: 0;
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-gap: 20px;
  max-width: 400px;
  margin: 60px auto;

  &__list {
    list-style-type: none;
    background: white;
    padding: 30px;
    border-radius: 10px;
    box-shadow: 1px 3px 5px rgba(0, 0, 0, 0.1);
    cursor: pointer;
    line-height: 1.5em;
  }
}
</style>