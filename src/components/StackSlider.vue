<template>
    <div class="slider">
        <div class="track">
            <span v-for="(item, i) in stack" :key="i">
                {{ item }}
            </span>
        </div>
    </div>
</template>

<script>
export default {
    name: "StackSlider",
    data() {
        return {
            stack: [
                "Rust",
                "Solana",
                "Web3",
                "Smart Contracts",
                "AI",
                "React",
                "Javascript",
            ],
        };
    },
};
</script>

<style scoped>
.slider {
    overflow: hidden;
    margin-top: 1.5rem;
    height: 32px;
}

.track span {
    margin-right: 2rem;
    font-weight:600;
    opacity: 0.85 ;
}

@keyframes scroll {
    from {
        transform: translateX(0);
    }
    to {
        transform: translateX(-50%);
    }
}

.track {
    display: inline-block;
    white-space: nowrap;
    animation: scroll 20s linear infinite;
}

</style>