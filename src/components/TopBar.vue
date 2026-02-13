<template>
    <div class="top-bar"></div>
</template>

<script>
export default {
    name: "TopBar",
};
</script>

<style scoped>
.top-bar {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 50px;
    background: #000;
    z-index: 100;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.5);
}
</style>