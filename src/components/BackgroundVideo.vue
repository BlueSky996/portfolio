<template>
    <video
        class="bg-video"
        autoplay
        muted
        loop
        playsinline
    >
        <source src="../assets/background.mp4" type="video/mp4" />
     </video>
</template>

<script>
export default {
    name: "BackgroundVideo",
};
</script>

<style scoped>
.bg-video {
    position: fixed;
    inset: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
}
</style>