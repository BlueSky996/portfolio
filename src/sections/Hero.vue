<template>
    <section class="hero">
        <div class="hero-bg"> </div>


          <div class="hero-content">
            <div class="hero-text">
               <h1>{{ project?.title || "Mohamed Khasheebah"}}</h1>
                 <p>
                    {{ project?.tagline || "Web3 / Rust / Smart Contracts" }}
                 </p>


                <ul class="stats">
                    <li>
                        <span class="label">Role</span>
                        <span class="value">{{ project?.role || "Full-Stack Web3" }}</span>
                    </li>
                    <li>
                        <span class="label">Stack</span>
                        <span class="value">{{ project?.stack || "Rust . Solana . AI" }}</span>
                    </li>
                    <li>
                        <span class="label">Status</span>
                        <span class="value">{{ project?.status || "Active" }}</span>
                    </li>
                </ul>


            <StackSlider />
           </div>

           <div class="hero-visual">
               <img src="../assets/me.jpg" alt="Me" />
           </div>
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
        Mounted() {
        gsap.from(".hero", {
            opacity: 0,
            y: 40,
            duration: 1,
            ease: "power3.out",
        });
    },
};
</script>

<style scoped>

.hero * {
    transition: all 0.35s;
}

.hero {
    position: relative;
    height: 100vh;
    overflow: hidden;
    color: white;
}

.hero-content {
    position: relative;
    width: 100%;
    height: 100%;
}


.hero-text {
    position: relative;
    left: 8%;
    top: 50%;
    transform: translate(-50%);
    max-width: 520px;
    z-index: 2;
}

.hero-visual {
    position: absolute;
    right: 10%;
    bottom: 0;
    z-index: 1;
}

.hero-visual img {
    width: 360px;
    filter: drop-shadow(0 30px 40px rgba(0, 0, 0, 0.6));

}

.hero-visual img:hover {
    transform: translateY(-8px) scale(1.02);
    filter: drop-shadow(0 40px 60px rgba(0, 0, 0, 0.7))
}

.stats {
    display: flex;
    gap: 2rem;
    margin: 1.5rem 0 2rem;
    padding: 0;
    list-style: none;
}

.stats li {
    display: flex;
    flex-direction: column;
    font-size: 0.85rem;
}

.label {
    opacity: 0.6;
    text-transform: uppercase;
    font-size: 0.7rem;
    letter-spacing: 1px;
}

.value {
    font-weight: 600;
}
</style>