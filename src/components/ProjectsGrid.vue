<template>
    <section class="projects">
        <div
          v-for="(project, i) in projects"
          :key="project.title"
          class="project-card"
          @mouseenter="hoverIn(i)"
          @mouseleave="hoverOut(i)"
          @click="$emit(`select`, project)"
        >
          <div class="thumb">
            <img :src="project.image" alt="" />
          </div>
          
          <div class="meta">
            <h3>{{ project.title }}</h3>
            <p>{{ project.tagline }}</p>
          </div>
        </div>
    </section>
</template>

<script>

import { gsap } from "gsap";

export default {
    name: "ProjectsGrid",
    data() {
        return {
            projects: [
                {
                    title: "Schordinger",
                    tagline: "AI-drive twitter sentiment",
                    image: "/projects/one.png",
                    role: "Backend / AI",
                    stack: "Rust , Solana, NLP",
                    status: "Active",
                },
                {
                    title: "Wormhole xmsg",
                    tagline: "AI-drive twitter sentiment",
                    image: "/projects/one.png",
                    role: "Backend / AI",
                    stack: "Rust , Solana, NLP",
                    status: "Active",
                },
                {
                    title: "CoW protocol",
                    tagline: "AI-drive twitter sentiment",
                    image: "/projects/one.png",
                    role: "Backend / AI",
                    stack: "Rust , Solana, NLP",
                    status: "Active",
                },
            ],
        };
    },

    methods: {
        hoverIn(i) {
            gsap.to(this.$el.children[i], {
                y: -10, scale: 1.03, duration: 0.3, ease: "power3.out",
            });
        },
        hoverOut(i) {
            gsap.to(this.$el.children[i], {
                y:0, scale: 1, duration: 0.3, ease: "power3.out",
            });
        },
    },
};

</script>

<style scoped>
.projects {
    position: relative;
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
    gap: 2rem;
    padding: 3rem 6%;
    margin-top: 4rem;
}

.project-card {
    background: rgba(255, 255, 255, 0.06);
    border-radius: 18px;
    padding: 1.5rem;
    backdrop-filter: blur(14px);
    border: 1px solid rgba(255, 255, 255, 0.12);
    transition: transform 0.3s ease;
    cursor: pointer;
}

.project-card:hover {
    transform: translateY(-6px);
}

.thumb img {
    width: 100%;
    height: 160px;
    object-fit: cover;
}

.meta {
    padding: 1rem 1.2rem 1.4rem;
}

.meta h3 {
    font-size: 1.1rem;
    margin: 0;
}

.meta p {
    opacity: 0.8;
    font-size: 0.9rem;
    margin-top: 0.4rem;
}

</style>