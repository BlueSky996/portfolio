<template>
    <div class="cursor-trail">
      <div 
        v-for="(trail, i) in trails"
        :key="i"
        class="trail-particle"
        :style="{
            left: trail.x + 'px',
            top: trail.y + 'px',
            opacity: trail.opacity,
        }"
       ></div>
    </div>
</template>

<script>
export default {
    name: "CursorTrail",
    data() {
        return {
            trails: [],
            maxTrails: 10,
            mouseX: 0,
            mouseY: 0,
        };
    },
    mounted() {
        document.addEventListener("mousemove", this.handleMouseMove);
        this.animateTrails();
    },
    beforeUnmount() {
        document.removeEventListener("mousemove", this.handleMouseMove);
    },
    methods: {
        handleMouseMove(e) {
            this.mouseX = e.clientX;
            this.mouseY = e.clientY;

            // add new trail particle
            this.trails.push({
                x: e.clientX,
                y: e.clientY,
                opacity: 1,
            });

            if (this.trails.length > this.maxTrails) {
                this.trails.shift();
            }
        },

        animateTrails() {
            setInterval(() => {
                this.trails = this.trails.map(trail => ({
                    ...trail,
                    opacity: trail.opacity - 0.05,
                })).filter(trail => trail.opacity > 0);
            }, 30);
        },
    },

};
</script>

<style scoped>
.cursor-trail {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    pointer-events: none;
    z-index: 9999;
}

.trail-particle {
    position: absolute;
    width: 8px;
    height: 8px;
    border-radius: 50%;
    background: radial-gradient(
        circle at center,
        rgba(0, 240, 255, 0.8) 0%,
        rgba(0, 240, 255, 0.4) 50%,
        transparent 100%
    );
    box-shadow: 
        0 0 10px rgba(0, 240, 255, 0.6),
        0 0 20px rgba(0, 240, 255, 0.3);
    transform: translate(-50%, -50%);
    transition: opacity 0.3s ease-out;
}

/* Alternate colors */
.trail-particle:nth-child(3n) {
    background: radial-gradient(
        circle at center,
        rgba(255, 42, 42, 0.8) 0%,
        rgba(255, 42, 42, 0.4) 50%,
        transparent 100%
    );
    box-shadow: 
        0 0 10px rgba(255, 42, 42, 0.6),
        0 0 20px rgba(255, 42, 42, 0.3);
}

.trail-particle:nth-child(5n) {
    background: radial-gradient(
        circle at center,
        rgba(255, 204, 0, 0.8) 0%,
        rgba(255, 204, 0, 0.4) 50%,
        transparent 100%
    );
    box-shadow: 
        0 0 10px rgba(255, 204, 0, 0.6),
        0 0 20px rgba(255, 204, 0, 0.3);
}
</style>