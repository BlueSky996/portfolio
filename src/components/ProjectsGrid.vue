<template>
    <section class="projects">
        <h2 class="projects-title">PROJECTS</h2>

        <div class="projects-grid">
        <a
          v-for="(project, i) in projects"
          :key="project.title"
          :href="project.link"
          target="_blank"
          rel="noopener noreferrer"
          class="project-card"
          @mouseenter="hoverIn(i)"
          @mouseleave="hoverOut(i)"
        >

        <!--Slanted card wrapper -->
        <div class="slant-wrapper">
            <div class="project-image">
                <img :src="project.image" alt="project.title" />
                <div class="image-overlay"></div>
        </div>

        <!-- Info section with space for text-->
         <div class="project-content">
            <div class="rank-badge">
                <span class="rank-label">RANK</span>
                <span class="rank-num">{{ String(i + 1).padStart(2, '0')}}</span>
         </div>

         <!-- Project text info-->
          <div class="project-text">
            <span class="project-label">PROJECT NAME</span>
            <h3>{{ project.title }}</h3>
            <p class="description">{{ project.tagline }}</p>
          </div>
          </div>
        </div>
    </a>
    </div>
    </section>
</template>

<script>

import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
gsap.registerPlugin(ScrollTrigger);

export default {
    name: "ProjectsGrid",
    data() {
        return {
            projects: [
                {
                    title: "JustDropped",
                    tagline: "help people in general to catch good discount or deals by alerting them through email or by visiting our website and check for those deals",
                    image: "/src/assets/one.png",
                    stack: "Javascript, Python, CSS, HTML, React, FastAPI, Postgres",
                    link: "https://github.com/BlueSky996/JustDropped",
                },
                {
                    title: "Wormhole xmsg",
                    tagline: "It shows how a message can be published on one chain, verified by Wormhole guardians, and securely consumed on another chain.",
                    image: "/src/assets/two.jpg",
                    stack: "Solidity , Javascript",
                    link: "https://github.com/BlueSky996/wormhole-xmsg-scope",
                },
                {
                    title: "CoW protocol",
                    tagline: "off-chain intent aggregation concepts can be expressed using on-chain components such as an order book, a matching engine, and batch settlement logic.",
                    image: "/src/assets/three.jpg",
                    stack: "Solidity , Javascript",
                    link: "https://github.com/BlueSky996/CoW-BatchAuction-Prototype",
                },
                {
                    title: "My Portfolio",
                    tagline: "My Portfolio website.",
                    image: "/src/assets/four.png",
                    stack: "Javascript, Vue",
                    link: "https://github.com/BlueSky996/portfolio",
                },
                {
                    title: "ROTO",
                    tagline: "is a Solana smart contract built in Rust using the Solana Program framework. It implements a meme roll and launch cycle with phase control, cooldown logic, and on-chain state management.",
                    image: "/src/assets/five.png",
                    stack: "Rust , Solana, GSAP, Javascript",
                    link: "https://fgfdsd",
                },
            ],
        };
    },

          mounted() {  // Scroll Animations
            this.initScrollAnimations();
        },

    methods: {
        hoverIn(i) {
            const card = this.$el.querySelector('.projects-grid').children[i];
            gsap.to(card, {
                y: -15, duration: 0.3, ease: "power3.out",
            });
        },
        hoverOut(i) {
             const card = this.$el.querySelector('.projects-grid').children[i];
             gsap.to(card, {
                y: 0, duration: 0.3, ease: "power3.out",
            });
        },

        initScrollAnimations() {
            // animate title
            gsap.from(".projects-title", {
                scrollTrigger: {
                    trigger: ".projects-title",
                    start: "top 80%",
                    toggleActions: "play none none none",
                },
                y: 50,
                opacity: 0,
                duration: 1,
                ease: "power3.out",
            });

            //animate cards 
            gsap.from(".project-card", {
                scrollTrigger: {
                    trigger: ".projects-grid",
                    start: "top 80%",
                    toggleActions: "play none none none",
                },
                y: 100,
                opacity: 0,
                duration: 0.8,
                stagger: 0.2,  // delay between each cards
                ease: "power3.out",
            });
        }
    },
};

</script>

<style scoped>
.projects {
    position: relative;
    padding: 6rem 4%;
}

.projects-title {
    font-size: 5.5rem;
    font-weight: 900;
    text-align: center;
    margin-bottom: 15rem;
    text-transform: uppercase;
    letter-spacing: 15px;
    color: #fff;
    position: relative;
    text-shadow: 0 0 30px rgba(255, 42, 42, 0.5);
}


.projects-title::after {
    content: "";
    position: absolute;
    bottom: -1.5rem;
    left: 50%;
    transform: translateX(-50%);
    width: 150px;
    height: 5px;
    background: linear-gradient(90deg, #ff2a2a, #00f0ff);
    box-shadow: 0 0 15px rgba(255, 42, 42, 0.6);
}

.projects-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
    gap: 2.5rem;
    max-width: 1800px;
    margin: 0 auto;
}


.project-card {
    position: relative;
    cursor: pointer;
    text-decoration: none;
    color: inherit;
    display: block;
}

.slant-wrapper {
    position: relative;
    transform: skewY(-7deg);
    overflow: hidden;
    border: 3px solid rgba(255, 255, 255, 0.15);
    background: rgba(0, 0, 0, 0.7);
    backdrop-filter: blur(10px);
    box-shadow: 
        0 10px 40px rgba(0, 0, 0, 0.8),
        0 0 50px rgba(5, 238, 255, 0.3),
        inset 0 0 30px rgba(0, 0, 0, 0.5);
    transition: all 0.3s;
}

.project-card:hover .slant-wrapper {
    border-color: #00f0ff;
    box-shadow: 
        0 20px 60px rgba(0, 240, 255, 0.3),
        0 0 40px rgba(0, 240, 255, 0.5),
        0 0 80px rgba(0, 240, 255, 0.2),
        inset 0 0 30px rgba(0, 0, 0, 0.5);
}


.project-image {
    position: relative;
    width: 100%;
    height: 450px;  
    overflow: hidden;
}

.project-image img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transform: skewY(3deg) scale(1.04);
    transition: transform 0.5s ease;
    filter: brightness(0.8);
}

.project-card:hover .project-image img {
    transform: skewY(3deg) scale(1.15);
    filter: brightness(1);
}

/* Dark gradient overlay on image */
.image-overlay {
    position: absolute;
    inset: 0;
    background: linear-gradient(
        to bottom,
        transparent 0%,
        rgba(0, 0, 0, 0.3) 50%,
        rgba(0, 0, 0, 0.9) 100%
    );
    opacity: 0.8;
    pointer-events: none;
}


.project-content {
    position: relative;
    transform: skewY(3deg);
    padding: 1.5rem 1.5rem 2rem;
    min-height: 160px; 
}


.rank-badge {
    position: absolute;
    top: 1.5rem;
    left: 2rem;
    background: rgba(0, 0, 0, 0.95);
    padding: 0.5rem 1.2rem;
    clip-path: polygon(8px 0, 100% 0, calc(100% - 8px) 100%, 0 100%);
    border-left: 4px solid #ff2a2a;
    z-index: 2;
}

.rank-label {
    display: block;
    font-size: 0.55rem;
    letter-spacing: 2px;
    opacity: 0.6;
    text-transform: uppercase;
}

.rank-num {
    display: block;
    font-size: 2.8rem;
    font-weight: 900;
    color: #ff2a2a;
    line-height: 0.9;
    text-shadow: 
        0 0 15px rgba(255, 42, 42, 0.7),
        0 0 30px rgba(255, 42, 42, 0.4),
        0 0 50px rgba(255, 42, 42, 0.3);
}


.project-text {
    margin-top: 6rem;  
    padding-right: 1rem;
}

.project-label {
    display: block;
    font-size: 1.3rem;
    font-weight: 900;
    letter-spacing: 5.5px;
    opacity: 0.8;
    text-transform: uppercase;
    margin-bottom: 1.5rem;
    color: #00f0ff;
}

.project-text h3 {
    font-size: 1.8rem;
    font-weight: 900;
    margin: 0 0 1rem 0;
    text-transform: uppercase;
    letter-spacing: 2px;
    color: #fff;
    text-shadow:
        0 0 10px rgba(255, 255, 255, 0.4),
        0 0 20px rgba(255, 240, 255, 0.3);
    line-height: 1.2;
}


.description {
    font-size: 0.95rem;
    line-height: 1.6;
    opacity: 0.85;
    color: #e0e0e0;
    margin: 0;
    max-width: 90%; 
}




/*  Alternate glow colors for variety */
.project-card:nth-child(2n):hover .slant-wrapper {
    border-color: #ff2a2a;
    box-shadow: 
        0 20px 60px rgba(255, 42, 42, 0.4),         
        0 0 40px rgba(255, 42, 42, 0.5),
        0 0 80px rgba(255, 42, 42, 0.2),
        inset 0 0 50px rgba(255, 42, 42, 0.1);
}

.project-card:nth-child(3n):hover .slant-wrapper {
    border-color: #ffcc00;
    box-shadow: 
        0 20px 60px rgba(255, 204, 0, 0.4),         
        0 0 40px rgba(255, 204, 0, 0.5),
        0 0 80px rgba(255, 204, 0, 0.2),
        inset 0 0 50px rgba(255, 204, 0, 0.1);
}




/* ==
   RESPONSIVE
   === */
@media (max-width: 1024px) {
    .projects-grid {
        grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
        gap: 2.5rem;
    }
}

@media (max-width: 768px) {
    .projects-grid {
        grid-template-columns: 1fr;
        gap: 2rem;
    }

    .projects-title {
        font-size: 2rem;
    }

    .project-image {
        height: 200px;
    }

    .rank-num {
        font-size: 2.2rem;
    }

    .project-text h3 {
        font-size: 1.4rem;
    }

    .project-text {
        margin-top: 5rem;
    }
}
</style>