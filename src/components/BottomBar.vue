<template>
    <div class="bottom-bar"></div>
</template>

<script>
export default {
    name: "BottomBar",
};
</script>

<style scoped>
.bottom-bar {
    position: relative;
    width: 100%;
    height: 50px;
    background: #000;
    z-index: 10;
    box-shadow: 0 -2px 10px rgba(0, 0, 0, 0.5);
}
</style>