<template>
  <BackgroundVideo />
  <Hero :project="selectedProject" />
  <ProjectsGrid @select="selectedProject = $event" />
</template>

<script>
import BackgroundVideo from './components/BackgroundVideo.vue';
import ProjectsGrid from './components/ProjectsGrid.vue';
import Hero from "./sections/Hero.vue";

export default {
  components: { BackgroundVideo, Hero, ProjectsGrid },

  data() {
    return {
      selectedProject: null,
    };
  },

  mounted() {
    this.selectedProject = null;

  },
};
</script>
