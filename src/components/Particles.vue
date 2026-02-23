<template>
    <div class="particles">
        <span 
            class="particle" 
            v-for="n in 80" 
            :key="n"
            :style="getParticleStyle(n)"
        ></span>
    </div>
</template>

<script>
export default {
    name: "Particles",
    mounted() {
        
    },
    methods: {
        getParticleStyle(n) {
            // Generate random position and timing for each particle
            const left = (n * 1.25) % 100; // Spread across width
            const animationDelay = (n * 0.15) % 10; // Stagger start times
            const animationDuration = 8 + (n % 8); // Vary speed
            const size = n % 3 === 0 ? 3 : n % 2 === 0 ? 2 : 1; // Vary sizes
            
            return {
                left: `${left}%`,
                animationDelay: `${animationDelay}s`,
                animationDuration: `${animationDuration}s`,
                width: `${size}px`,
                height: `${size}px`,
            };
        },
    },
};
</script>

<style scoped>
.particles {
    position: fixed;
    inset: 0;
    width: 100%;
    height: 100%;
    overflow: hidden;
    pointer-events: none;
    z-index: 5;  /* ⭐ Above video (0) and video effects (1-3) */
}

.particle {
    position: absolute;
    top: -10px;
    background: rgba(255, 255, 255, 0.7);
    border-radius: 50%;
    animation: particleFall linear infinite;
    box-shadow: 0 0 4px rgba(255, 255, 255, 0.5);
}

@keyframes particleFall {
    0% {
        transform: translateY(0) translateX(0);
        opacity: 0;
    }
    10% {
        opacity: 1;
    }
    80% {
        opacity: 0.8;
    }
    100% {
        transform: translateY(105vh) translateX(calc(sin(1) * 30px));
        opacity: 0;
    }
}
</style>