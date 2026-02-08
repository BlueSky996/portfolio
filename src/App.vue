<template>
  <BackgroundVideo />
  <Hero />
  <ProjectsGrid />
</template>

<script>
import BackgroundVideo from './components/BackgroundVideo.vue';
import ProjectsGrid from './components/ProjectsGrid.vue';
import Hero from "./sections/Hero.vue";

export default {
  components: { BackgroundVideo, Hero, ProjectsGrid },
};
</script>

