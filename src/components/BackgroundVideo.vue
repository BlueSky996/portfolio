<template>
    <div class="bg-video-wrapper">
    <video
        class="bg-video"
        autoplay
        muted
        loop
        playsinline
    >
        <source src="../assets/background.mp4" type="video/mp4" />
     </video>
     <div class="glass-k">K</div>
     <div class="dot-pattern"></div>
     <div class="vignette"></div>
     </div>
</template>

<script>
export default {
    name: "BackgroundVideo",
};
</script>

<style scoped>

.bg-video-wrapper {
    position: fixed;
    inset: 0;
    width: 100%;
    height: 100vh;
    z-index: 0;
}

.bg-video {
    position: absolute;
    inset: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
    opacity: 0.3;
    filter: blur(1px);
}

.vignette {
    position: absolute;
    inset: 0;
    width: 100%;
    height: 100%;
    background: radial-gradient(
        circle at center,
        transparent 0%,
        transparent 40%,
        rgba(0, 0, 0, 0.4) 70%,
        rgba(0, 0, 0, 0.8) 100%
    );
    pointer-events: none;
}

.glass-k {
    position: absolute;
    top: 50%;
    left: 75%;
    transform: translate(-50%, -50%);
    font-size: 110rem;
    font-weight: 900;
    font-family: -apple-system, sans-serif;
    color: transparent;
    -webkit-text-stroke: 2px rgba(255, 255, 255, 0.38); /* Subtle outline */
    text-shadow: 0 0 40px rgba(0, 0, 0, 0.5);
    opacity: 0.9;
    mix-blend-mode: overlay;
    pointer-events: none;
    z-index: 1;
}

/* Dot pattern */
.dot-pattern {
    position: absolute;
    inset: 0;
    width: 100%;
    height: 100%;
    background-image: radial-gradient(
        circle at center,
        rgba(255, 255, 255, 0.6) 1px,
        transparent 1px
    );
    background-size: 4px 4px;
    opacity: 0.4;
    pointer-events: none;
    z-index: 2;
}
</style>