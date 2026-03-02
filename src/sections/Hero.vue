<template>
    <section class="hero">

          <div class="hero-content"> 
            
            <!-- left side + Visual + Geometry-->
             <div class="hero-left">
                <!-- Cv Label overly -->
                <div class="hero-cv">
                    <span class="cv-label">CV</span>
                    <span class="cv-name">Mohamed Khasheebah</span>
                </div>

            <!-- Geometric background -->
             <div class="hero-geometry"></div>

            <!-- Visual -->
             <div class="hero-visual">
                <img src="../assets/me.png" alt="Me"/>
             </div>
             </div>

             <!-- Right Side - Content -->
            <div class="hero-right">

                <div class="hero-rank">
                    <span class="rank-label">Ranking NO</span>
                    <span class="rank-number">01</span>
                </div>

            <!-- Black angled title box -->
             <div class="hero-title-box">
                <h1>{{ project?.title || "Full-Stack & Blockchain Engineer" }}</h1>
             </div>

            <!-- Description -->
             <p class="hero-description">
                {{ project?.description || 
                   "Full-stack developer experienced in Python, Rust, Solidity, and modern frontend frameworks, building performant web and on-chain systems." }}
             </p>


             <!-- Reserved Media Area -->
              <div class="certificates-showcase">
                  <div class="showcase-header">
                    <span class="cert-label">CERTIFICATIONS</span>
                  </div>

                  <div class="cert-grid">
                    <div
                         v-for="(cert, i) in certificates"
                         :key="i"
                        class="cert-card"
                        @click="openCertificate(cert.link)"
                    >
                        <div class="cert-badge">
                           <img :src="cert.logo" :alt="cert.issuer" class="cert-logo" />
                         </div>
                        <div class="cert-info">
                        <h4>{{ cert.title }}</h4>
                        <p>{{ cert.issuer }}</p>
                        </div>
                        <div class="cert-arrow">→</div>
                    </div>
                </div>
                </div>
            </div>
            </div>



            <!-- STACK -->
             <div class="hero-stack">
                <StackSlider />
             </div>
    </section>
</template>



<script>
import { gsap } from "gsap";
import StackSlider from '../components/StackSlider.vue';

export default {
    name: "Hero",
    components: { StackSlider },
    props: {
        project: Object,
    },

    data() {
        return {
            certificates: [
                {
                    title: "Bachelor's Degree",
                    issuer:"UOT Information Technology - Network Engineering",
                    logo: "/src/assets/logos/it.jpg",
                    link:""
                },
                {
                    title:"CS50x - Computer Science",
                    issuer: "Harvard University",
                    logo: "/src/assets/logos/harvard.png",
                    link:""
                },
                {
                    title: "Cyfrin web3 ",
                    issuer: "Blockchain Development",
                    logo: "/src/assets/logos/cyfrin.png",
                    link:""
                },
            ]
        };
    },


    watch: {
        project() {
            this.animateSwap();
        },
    },
        mounted() {
            this.animateIn();
        }, 
        methods: {
            animateIn() {
            const tl = gsap.timeline({ defaults: { ease: "power3.out" } });

            // Set initial state to prevent disappearing issue
            gsap.set([".hero-geometry", ".hero-visual img", ".hero-cv", ".rank-number", ".hero-title-box h1", ".hero-description"], {
                clearProps: "all"
            });

            tl.from(".hero-title-box h1", { x: 50, opacity: 0, duration: 1 })
            .from(".hero-description", { y: 30, opacity: 0, duration: 0.8 },"-=0.6")
            .from(".rank-number",{ y: -30, opacity: 0, stagger: 0.15, duration: 0.6 },"-=0.5")
            .from(".hero-visual img",{ x: -100, opacity: 0, scale: 0.95, duration: 1 },"-=0.8")
            .from(".hero-geometry", { scale: 0, rotation: -45, opacity: 0, duration: 1.2 })
      },

    animateOut(onComplete) {
        gsap.to(
            [".hero-title-box h1", ".hero-description p", ".hero-rank", ".hero-visual img"],
            {y: -20, opacity: 0, stagger: 0.05, duration: 0.3, onComplete}
        );
    },

    animateSwap() {
        this.animateOut(() => {
            this.$nextTick(() => this.animateIn());
            });
        },

    openCertificate(link) {
        if (link) {
            window.open(link, "_blank");
           }
        }
    },
};

</script>



<style scoped>


.hero {
    position: relative;
    display: flex;
    flex-direction: column;
    min-height: 100vh;
    width: 100%;
    overflow: hidden;
    padding: 0 6vw;
    box-sizing: border-box;
    
}


.hero::before {
  content: "K";
  position: absolute;
  top: 8%;
  left: 3%;
  font-size: 30rem;
  font-weight: 900;
  opacity: 0.5;
  z-index: 0;
  line-height: 1;
}

.hero::after {
    content: "";
    position: absolute;
    right: -15%;
    top: -10;
    width: 70%;
    height: 120%;
    background: linear-gradient(135deg, rgba(255,255,255,0.04), transparent 60%);
    transform: skewX(-15deg);
    z-index: 0;
    pointer-events: none;
}


.hero-content {
    position: relative;
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 100%;
    flex: 1;
    padding: 80px 0;
    gap: 6rem;
    z-index: 2;
}


.hero-geometry {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%) rotate(-15deg);
    width: 1000px;
    height: 1000px;
    background:
        conic-gradient(from 0deg at 50% 50%,
             #ff0080 0deg,
             #00f0ff 60deg,
             #ffff00 120deg,
             #ff0080 180deg,
             #00ff00 240deg,
             #ff0080 300deg,
             transparent 360deg
        ),
        radial-gradient(circle, rgba(255,0,128,0.3) 0%, transparent 70%);
    mix-blend-mode: screen;
    opacity: 0.4;
    z-index: 1;
    pointer-events: none;
    filter: blur(2px);
    visibility: visible !important;
}


/* Alternative: More geometric/sharp explosion */
.hero-geometry::before,
.hero-geometry::after {
    content: "";
    position: absolute;
    top: 50%;
    left: 50%;
    width: 100%;
    height: 100%;
    transform: translate(-50%, -50%);
}

.hero-geometry::before {
    background: 
        linear-gradient(45deg, transparent 40%, #ff0080 40%, #ff0080 60%, transparent 60%),
        linear-gradient(-45deg, transparent 40%, #00f0ff 40%, #00f0ff 60%, transparent 60%);
    opacity: 0.6;
}

.hero-geometry::after {
    background: 
        linear-gradient(90deg, transparent 45%, #ffff00 45%, #ffff00 55%, transparent 55%),
        linear-gradient(0deg, transparent 45%, #00ff88 45%, #00ff88 55%, transparent 55%);
    opacity: 0.4;
    transform: translate(-50%, -50%) rotate(30deg);
}



.hero-visual {
    position: relative;
    display: flex;
    justify-content: flex-end;
    align-items: center;
    z-index: 3;
}

.hero-visual img {
    width: auto;
    height: 88vh;
    object-fit: contain;
    filter: 
          drop-shadow(0 30px 40px rgba(0, 0, 0, 0.6))
          drop-shadow(0 20px 60px rgba(0, 0, 0, 0.8));
    transform-origin: center bottom;
    transition: transform 0.5s cubic-bezier(0.35, 1.56, 0.64, 1), filter 0.35s;
}

.hero-visual img:hover {
    transform: translateY(-8px) scale(1.02);
    filter: drop-shadow(0 40px 60px rgba(0, 0, 0, 0.7));
    transition: transform 0.35s filter 0.35s;
}


.hero-left {
    position: relative;
    flex: 1;
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: 75vh;
}

.hero-cv {
    position: absolute;
    top: 16%;
    left: 10%;
    display: flex;
    gap: 0.8rem;
    align-items: center;
    font-size: 2rem;
    z-index: 5;
    background: rgba(0, 0, 0, 0.6);
    padding: 0.5rem 1.2rem;
    backdrop-filter: blur(4px);
}

.cv-label {
    color: #ff0000;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 1px;
}

.cv-name {
    font-weight: 600;
    color: #fff;
}

/* RIGHT SIDE */

.hero-right {
    flex: 1;
    position: relative;
    max-width: 550px;
    display: flex;
    flex-direction: column;
    z-index: 3;
    padding-right: 2rem;
}

/* ranking */

.hero-rank {
    position: absolute;
    top: -40;
    right: 0;
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    line-height: 1;
}

.rank-label {
    font-size: 1.5rem;
    letter-spacing: 2px;
    opacity: 0.6;
    text-transform: uppercase;
    font-weight: 900;
    margin-bottom: 0.5rem;
    color:#00f0ff;
}

.rank-number {
    visibility: visible !important;
    font-size: clamp(5rem, 10vw, 9rem);
    font-weight: 800;
    color: #ff2a2a;
    line-height: 0.85;
    text-shadow: 
          0 0 20px rgba(255, 0, 0, 0.5),
          0 0 40px rgba(255, 0, 0, 0.4);
}


/* Black Title Box */
.hero-title-box {
    position: relative;
    margin-top: 140px;
    background: black;
    padding: 1.8rem 2.5rem;
    clip-path: polygon(0 0, 100% 0, 92% 100%, 0% 100%);
    border-left: 4px solid #ff0000;
}


.hero-title-box::before {
    content: "";
    position: absolute;
    top: 0;
    right: 0;
    width: 8px;
    height: 100%;
    background: linear-gradient(to bottom, #ff0000, transparent);
    clip-path: polygon(0 0, 100% 0, 0 100%);
}


.hero-title-box h1 {
    font-size: 2.8rem;
    font-weight: 700;
    margin: 0;
    letter-spacing: 0.5px;
    color: white;
}


/* Description */
.hero-description {
    margin-top: 2.1rem;
    line-height: 1.6;
    opacity: 0.85;
    font-size: 2.5rem;
    color: #ffffff;
}

/* Reserved media area */
.hero-media-placeholder {
    margin-top: 2rem;
    height: 180px;
    border: 1px solid rgba(255,255,255,0.2);
    background: rgba(255, 255, 255, 0.02);
    position: relative;
    overflow: hidden;
}

.hero-stack {
    position: absolute;
    bottom: 100px;
    left: 0;
    right: 0;
    z-index: 4;
    padding: 0 4vw;
}


/* Certificates */
.certificates-showcase {
    margin-top: 1rem;
    margin-bottom: 5rem;
    background: rgba(0, 0, 0, 0.6);
    border: 2px solid rgba(0, 240, 255, 0.2);
    backdrop-filter: blur(15px);
    padding: 1.5rem;
    clip-path: polygon(0 0, 100% 0, calc(100% - 25px) 100%, 0 100%);
    box-shadow:
        0 0 80px rgba(9, 239, 255, 0.685),
        inset 0 0 10px rgb(8, 148, 241);
}

.showcase-header {
    display: flex;
    align-items: center;
    gap: 0.8rem;
    margin-bottom: 1.2rem;
    padding-bottom: 0.8rem;
    border-bottom: 1px solid rgba(255, 255, 255, 0.1);
}



.cert-label {
    font-size: 2.2rem;
    font-weight: 900;
    letter-spacing: 2px;
    opacity: 0.9;
    text-transform: uppercase;
    font-weight: 700;
    color: #00eeff;
}

.cert-card {
    display: flex;
    align-items: center;
    gap: 1rem;
    padding: 0.8rem 1rem;
    background: rgba(0, 0, 0, 0.557);
    border: 1px solid rgba(255, 255, 255, 0.1);
    border-left: 3px solid #00f0ff;
    cursor: pointer;
    transition: all 0.3s;
    clip-path: polygon(0 0, 100% 0, calc(100% - 8px) 100%, 0 100%);
}

.cert-card:hover {
    background: rgba(0, 240, 255, 0.1);
    border-color: #00f0ff;
    transform: translateX(5px);
    box-shadow: 0 4px 15px rgba(0, 240, 255, 0.2);
}

/* Alternate colors */
.cert-card:nth-child(2n) {
    border-left-color: #ff2a2a;
}

.cert-card:nth-child(2n):hover {
    background: rgba(255, 42, 42, 0.1);
    border-color: #ff2a2a;
    box-shadow: 0 4px 15px rgba(255, 42, 42, 0.2);
}

.cert-card:nth-child(3n) {
    border-left-color: #ffcc00;
}

.cert-card:nth-child(3n):hover {
    background: rgba(255, 204, 0, 0.1);
    border-color: #ffcc00;
    box-shadow: 0 4px 15px rgba(255, 204, 0, 0.2);
}


/* Badge icon */
.cert-badge {
    flex-shrink: 0;
    width: 45px;
    height: 45px;
    background: rgba(255, 255, 255, 0.05);
    border-radius: 8px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1.3rem;
}

.cert-logo {
    width: 100%;
    height: 100%;
    object-fit: contain;  /* Fit logo without distortion */
    filter: brightness(1.1);  /* Make logos pop */
    transition: transform 0.3s;
}

.cert-card:hover .cert-logo {
    transform: scale(1.1);  /* Slight zoom on hover */
}

/* Certificate info */
.cert-info {
    flex: 1;
}

.cert-info h4 {
    font-size: 1.5rem;
    font-weight: 700;
    margin: 0 0 0.3rem 0;
    color: #fff;
}

.cert-info p {
    font-size: 1.15rem;
    margin: 0;
    line-height: 1.3;
    color: #ff0000
}

/* Arrow indicator */
.cert-arrow {
    flex-shrink: 0;
    font-size: 1.2rem;
    opacity: 0.8;
    color: #fff;
    transition: all 0.3s;
}

.cert-card:hover .cert-arrow {
    opacity: 1;
    transform: translateX(3px);
}


/* Responsive */
/* ============================================
   (1024px and below)
   ============================================ */
@media (max-width: 1024px) {
    .hero-content {
        gap: 3rem;
    }

    .hero::before {
        font-size: 20rem;  /* Smaller K watermark */
    }

    .hero-visual img {
        height: 70vh;
        justify-content: center;
    }

    .hero-geometry {
        width: 700px;
        height: 700px;
    }

    .hero-title-box h1 {
        font-size: 2.2rem;
    }

    .hero-description {
        font-size: 1rem;
    }

    .rank-number {
        font-size: clamp(4rem, 8vw, 7rem);
    }
}

/* ============================================
   (768px and below)
   ============================================ */
@media (max-width: 768px) {
    .hero {
        padding: 0 4vw;
    }

    .hero-content {
        flex-direction: column;
        padding: 60px 0;
        gap: 2rem;
    }

    .hero-left,
    .hero-right {
        max-width: 100%;
        width: 100%;
    }

    .hero-left {
        min-height: 50vh;
        padding-left: 0;
        order: 1;  /* Character first */
    }

    .hero-visual img {
        height: 50vh;
        max-height: 500px;
        margin-left: 200px;
    }

    .hero-cv {
        top: 5%;
        left: 5%;
        font-size: 0.9rem;
        padding: 0.4rem 1rem;
    }

    .hero-geometry {
        width: 500px;
        height: 500px;
    }

    .hero::before {
        font-size: 12rem;
        top: 5%;
        left: 0;
    }

    .hero-right {
        order: 2;  /* Content second */
        padding-right: 0;
    }

    .hero-rank {
        position: relative;
        top: 0;
        align-items: center;
        text-align: center;
        margin-bottom: 2rem;
    }

    .rank-label {
        font-size: 0.8rem;
    }

    .rank-number {
        font-size: 5rem;
    }

    .hero-title-box {
        margin-top: 0;
    }

    .hero-title-box h1 {
        font-size: 1.8rem;
    }

    .hero-description {
        font-size: 0.95rem;
        margin-top: 1.5rem;
    }

    .certificates-showcase {
        margin-top: 1.5rem;
    }

    .hero-stack {
        position: relative;
        bottom: 0;
        left: 0;
        right: 0;
        margin-top: 3rem;
        padding: 0;
    }
}

/* ============================================
   (480px and below)
   ============================================ */
@media (max-width: 480px) {
    .hero {
        padding: 0 3vw;
    }

    .hero-visual img {
        height: 40vh;
        margin-left: 200px;
        transform: translateX(0);
    }

    .hero-cv {
        font-size: 0.75rem;
        padding: 0.3rem 0.8rem;
        gap: 0.5rem;
    }

    .hero-geometry {
        width: 350px;
        height: 350px;
    }

    .hero::before {
        font-size: 8rem;
    }

    .rank-label {
        font-size: 0.65rem;
        letter-spacing: 1px;
    }

    .rank-number {
        font-size: 3.5rem;
    }

    .hero-title-box {
        padding: 1.2rem 1.5rem;
    }

    .hero-title-box h1 {
        font-size: 1.4rem;
    }

    .hero-description {
        font-size: 0.85rem;
        line-height: 1.5;
    }

    .cert-card {
        padding: 0.6rem 0.8rem;
        gap: 0.8rem;
    }

    .cert-badge {
        width: 35px;
        height: 35px;
    }

    .cert-logo {
        width: 100%;
        height: 100%;
    }

    .cert-info h4 {
        font-size: 0.8rem;
    }

    .cert-info p {
        font-size: 0.65rem;
    }

    .showcase-header {
        margin-bottom: 1rem;
    }

    .cert-label {
        font-size: 0.6rem;
    }
}

/* ============================================
   (360px and below)
   ============================================ */
@media (max-width: 360px) {
    .hero-title-box h1 {
        font-size: 1.2rem;
    }

    .hero-description {
        font-size: 0.8rem;
    }

    .rank-number {
        font-size: 3rem;
    }

    .hero-visual img {
        height: 35vh;
        justify-content: center;
    }
}



</style>