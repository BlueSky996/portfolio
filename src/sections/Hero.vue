<template>
    <section class="hero">
        <div class="glass">
          <div class="hero-left">
             <h1>{{ project?.title || "Mohamed Khasheebah"}}</h1>
                <p>
                   {{ project?.tagline || "Web3 / Rust / Smart Contracts" }}
                </p>

            <StackSlider />
           </div>

           <div class="hero-right">
               <img src="/images/me.png" alt="Me" />
           </div>
        </div>
    </section>
</template>

<script>
import StackSlider from '../components/StackSlider.vue';

export default {
    name: "Hero",
    components: { StackSlider },
    props: {
        project: Object,
    },
};
</script>

<style scoped>

.hero {
    min-height: 100vh;
    display: flex;
    grid-template-columns: 1.2fr 1fr;
    align-items: center;
    padding: 4rem;
    color: white;
}

.glass {
    display: flex;
    gap: 4rem;
    padding: 3rem 4rem;
    border-radius: 24px;
    background: rgba(255, 255, 255, 0.08);
    backdrop-filter: blue(16px);
    -webkit-backdrop-filter: blur(16px);
    border: 1px solid rgba(255, 255, 255, 0.15);
    box-shadow: 0 20px 50px rgba(0, 0, 0, 0.4);
}

.hero-left {
    max-width: 600px;
}

.hero-left h1 {
    font-size: 3rem;
    margin-bottom: 1rem;
}

.hero-left p {
    opacity: 0.9;
    line-height: 1.6;
}

.hero-right img {
    width: 320px;
    filter: drop-shadow(0 30px 40px rgba(0, 0, 0, 0.6));
    transition: transform 0.4 ease, filter 0.4s ease;
    will-change: transform;
}

.hero-right img:hover {
    transform: translateY(-8px) scale(1.02);
    filter: drop-shadow(0 40px 60px rgba(0, 0, 0, 0.7))
}
</style>