<template>
    <section class="projects">
        <div
          v-for="project in projects"
          :key="project.title"
          class="project-card"
          @click="$emit(`select`, project)"
        >
          <img :src="project.image" alt="" />
          <h3>{{ project.title }}</h3>
          <p>{{ project.tagline }}</p>
        </div>
    </section>
</template>

<script>
export default {
    name: "ProjectsGrid",
    data() {
        return {
            projects: [
                {
                    title: "Schordinger",
                    tagline: "AI-drive twitter sentiment",
                    image: "/projects/one.png",
                },
                {
                    title: "Wormhole xmsg",
                    tagline: "AI-drive twitter sentiment",
                    image: "/projects/one.png",
                },
                {
                    title: "CoW protocol",
                    tagline: "AI-drive twitter sentiment",
                    image: "/projects/one.png",
                },
            ],
        };
    },
};

</script>

<style scoped>
.projects {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
    gap: 2rem;
    padding: 4rem 6rem;
}

.projects-card {
    background: rgba(255, 255, 255, 0.06);
    border-radius: 18px;
    padding: 1.5rem;
    backdrop-filter: blur(14px);
    border: 1px solid rgba(255, 255, 255, 0.12);
    transition: transform 0.3s ease;
}

.projects-card hover {
    transform: translate(-6px);
}

.projects-card img {
    width: 100%;
    border-radius: 12px;
    margin-bottom: 1rem;
}

.projects-card h3 {
    margin: 0;
}

.projects-card p {
    opacity: 0.8;
    font-size: 0.9rem;
}

</style>