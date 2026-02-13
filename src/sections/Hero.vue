<template>
    <section class="hero">
        <div class="hero-top-bar"></div>


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
                <img src="../assets/me.jpg" alt="Me"/>
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
                <h1>{{ project?.title || "Top Web3 Engineer" }}</h1>
             </div>

            <!-- Description -->
             <p class="hero-description">
                {{ project?.description || 
                   "Full stack developer focusing on web3 technologies and future" }}
             </p>


             <!-- Reserved Media Area -->
              <div class="hero-media-placeholder">
                <!-- Future content here -->
              </div>
            </div>
            </div>



            <!-- STACK -->
             <div class="hero-stack">
                <StackSlider />
             </div>

             <!-- FOOTER BAR -->
              <div class="hero-bottom-bar"></div>
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
            tl.from(".hero-title-box h1", { x: 50, opacity: 0, duration: 1 })
            .from(".hero-description", { y: 30, opacity: 0, duration: 0.8 },"-=0.6")
            .from(".hero-rank",{ y: 30, opacity: 0, stagger: 0.15, duration: 0.6 },"-=0.5")
            .from(".hero-visual img",{ y: 80, opacity: 0, scale: 0.95, duration: 1 },"-=0.8")
            .from(".hero-geometry", { scale: 0, rotation: -45, opacity: 0, duration: 1.2 })
            .from(".hero-visual img", { x: -100, opacity: 0, scale: 0.9, duration: 1 }, "-=0.8");
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
    },
};

</script>



<style scoped>

.hero * {
    transition: all 0.35s;
}

.hero {
    position: relative;
    display: flex;
    flex-direction: column;
    min-height: 100vh;
    width: 100%;
    overflow: hidden;
    padding: 0 6vw;
    box-sizing: border-box;

    background:
    radial-gradient(circle at 30% 50%, rgba(255,255,255,0.06), transparent 50%),
    linear-gradient(to right, rgba(255,255,255,0.03) 1px, transparent 1px),
    #0e0e0e;

    background-size: auto, 50px 50px, auto;
    
}


.hero::before {
  content: "X";
  position: absolute;
  top: 8%;
  left: 3%;
  font-size: 30rem;
  font-weight: 900;
  opacity: 0.03;
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
    width: 600px;
    height: 600px;
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
    filter: drop-shadow(0 40px 60px rgba(0, 0, 0, 0.7))
}



.hero-top-bar,
.hero-bottom-bar {
    position: absolute;
    left: 0;
    width: 100%;
    height: 80px;
    background: #000;
    z-index: 10;
}

.hero-top-bar {
    top: 0;
}

.hero-bottom-bar {
    bottom: 0;
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
    top: 8%;
    left: 10%;
    display: flex;
    gap: 0.8rem;
    align-items: center;
    font-size: 1rem;
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
    font-size: 0.7rem;
    letter-spacing: 2px;
    opacity: 0.6;
    text-transform: uppercase;
    font-weight: 600;
    margin-bottom: 0.5rem;
}

.rank-number {
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
    font-size: 1.8rem;
    font-weight: 700;
    margin: 0;
    text-transform: lowercase;
    letter-spacing: 0.5px;
}


/* Description */
.hero-description {
    margin-top: 2.5rem;
    line-height: 1.6;
    opacity: 0.85;
    font-size: 1rem;
    color: #e0e0e0;
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
    bottom: 6vh;
    left: 6vw;
    z-index: 11;
}





</style>