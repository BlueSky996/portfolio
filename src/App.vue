<template>
  <main class="stage">
  <BackgroundVideo />
  <TopBar />
  <Hero :project="selectedProject" />
  <ProjectsGrid @select="selectedProject = $event" />
  <BottomBar />
  </main>
</template>

<script>
import TopBar from './components/TopBar.vue';
import BottomBar from './components/BottomBar.vue';
import BackgroundVideo from './components/BackgroundVideo.vue';
import ProjectsGrid from './components/ProjectsGrid.vue';
import Hero from "./sections/Hero.vue";

export default {
  components: { TopBar, BottomBar, BackgroundVideo, Hero, ProjectsGrid },

  data() {
    return {
      selectedProject: null,
    };
  },

};
</script>

<style>

.stage {
  position: relative;
  width: 100%;
  overflow-x: hidden;
}
</style>
