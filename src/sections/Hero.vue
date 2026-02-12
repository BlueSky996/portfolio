<template>
    <section class="hero">

        <div class="hero-top-bar"></div>


          <div class="hero-content"> 
            
            <!-- left side -->
             <div class="hero-left">
                <div class="hero-cv">
                    <span class="cv-label">CV</span>
                    <span class="cv-name">Mohamed Khasheebah</span>
                </div>

            <!-- Visual -->
             <div class="hero-visual">
                <img src="../assets//me.jpg" alt="Me"/>
             </div>

             </div>

             <!-- Right Side-->
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
            tl.from(".hero-text h1", { y: 50, opacity: 0, duration: 1, })
            .from(".hero-text p", { y: 40, opacity: 0, duration: 0.8 },"-=0.6")
            .from(".stats li",{ y: 30, opacity: 0, stagger: 0.15, duration: 0.6 },"-=0.5")
            .from(".hero-visual img",{ y: 80, opacity: 0, scale: 0.95, duration: 1 },"-=0.8");
      },

    animateOut(onComplete) {
        gsap.to(
            [".hero-text h1", ".hero-text p", ".stats li", ".hero-visual img"],
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
    min-height: 100vh;
    width: 100vw;
    overflow: hidden;
    padding: 0 8vw;
    align-items: center;
    box-sizing: border-box;

    background:
    radial-gradient(circle at 70% 40%, rgba(255,255,255,0.06), transparent 60%),
    linear-gradient(to right, rgba(255,255,255,0.03) 1px, transparent 1px),
    #0e0e0e;

    background-size: auto, 40px 40px, auto;
    
}


.hero::before {
  content: "X";
  position: absolute;
  top: 10%;
  left: 6%;
  font-size: 14rem;
  font-weight: 900;
  opacity: 0.04;
  z-index: 0;
}


.hero-content {
    position: relative;
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 100%;
    padding-top: 80px;
    padding-bottom: 80px;
    z-index: 2;
}


.hero-text {
    flex: 1;
    max-width: 520px;
    z-index: 3;
}

.hero-text h1 {
    font-size: clamp(3rem, 6vw, 6rem);
    line-height: 1.05;
    font-weight: 700;
    letter-spacing: -1px;
}

.hero-text p {
    font-size: 1.1rem;
    margin-top: 1.2rem;
    line-height: 1.6;
    opacity: 0.9;
}

.hero-visual {
    position: relative;
    display: flex;
    flex: 1;
    justify-content: flex-end;
    align-items: center;
    z-index: 2;
}

.hero-visual img {
    width: auto;
    height: 85vh;
    object-fit: contain;
    filter: drop-shadow(0 30px 40px rgba(0, 0, 0, 0.6));
    transform-origin: center;
    transition: transform 0.35s, filter 0.35s;
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
}

.hero-cv {
    position: absolute;
    top: 5%;
    left: 5%;
    display: flex;
    gap: 1rem;
    align-items: center;
    font-size: 1rem;
    z-index: 5;
}

.cv-label {
    color: red;
    font-weight: 700;
}

.cv-name {
    font-weight: 600;
}

/* RIGHT SIDE */

.hero-right {
    flex: 1;
    position: relative;
    max-width: 550px;
}

/* ranking */

.hero-rank {
    position: absolute;
    top: 0;
    right: 0;
    text-align: right;
}

.rank-label {
    font-size: 0.7rem;
    letter-spacing: 2px;
    opacity: 0.6;
}

.rank-number {
    font-size: 5rem;
    font-weight: 800;
    color: #ff2a2a;
}


/* Black Title Box */
.hero-title-box {
    margin-top: 120px;
    background: black;
    padding: 1.5rem 2rem;
    clip-path: polygon(0 0, 100% 0, 92% 100%, 0% 100%);
}

.hero-title-box h1 {
    font-size: 1.8rem;
    font-weight: 700;
}


/* Description */
.hero-description {
    margin-top: 2rem;
    line-height: 1.6;
    opacity: 0.85;
}

/* Reserved media area */
.hero-media-placeholder {
    margin-top: 2rem;
    height: 180px;
    border: 1px solid rgba(255,255,255,0.2)
}

.hero-stack {
    position: absolute;
    bottom: 6vh;
    left: 6vw;
    z-index: 4;
}

.stats {
    display: flex;
    gap: 2.5rem;
    margin-top: 2rem;
    list-style: none;
}

.stats li {
    display: flex;
    flex-direction: column;
}

.label {
    opacity: 0.6;
    text-transform: uppercase;
    font-size: 0.7rem;
    letter-spacing: 1px;
    margin-bottom: 0.2rem;
}

.value {
    font-weight: 600;
    font-size: 0.85rem;
}




</style>