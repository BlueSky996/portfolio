<template>
    <div class="slider">
        <div class="track">
            <span v-for="(item, i) in [...stack, ...stack]" 
            :key="i"
            class="stack-item"
            >
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
                "Typescript",
                "Web3",
                "Smart Contracts",
                "AI",
                "React",
                "Javascript",
                "Solidity",
                "Python",
                "Vue",
                "PostgreSQL",
                "MongoDB",
                "AWS",
                "DynamoDB",
                "FastAPI",
                "Alpine.js",
                "tailwind",
                "RESTful API",
            ],
        };
    },
};
</script>

<style scoped>
.slider {
    position: relative;
    overflow: hidden;
    display: flex;
    align-items: center;
    background: rgba(0, 0, 0, 0.4);
    backdrop-filter: blur(10px);
    border: 1px solid rgba(255, 255, 255, 0.12);
    border-left: 3px solid #00f0ff;
    padding: 0 2rem;
    box-shadow: 
        0 0 20px rgba(0, 240, 255, 0.1),
        inset 0 0 20px rgba(0, 240, 255, 0.05);
    margin-top: 1.5rem;
    height: 50px;
}

.slider::before {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: linear-gradient(
        90deg,
        transparent 0%,
        rgba(0, 240, 255, 0.1) 50%,
        transparent 100%
    );
    animation: shimmer 3s linear infinite;
    pointer-events: none;;
}

.track {
    display: flex;
    gap: 3rem;
    animation: scroll 30s linear infinite;
    will-change: transform;
}

.stack-item {
    display: inline-flex;
    align-items: center;
    font-weight: 700;
    font-size: 1.55rem;
    letter-spacing: 1px;
    color: #fff;
    text-transform: uppercase;
    white-space: nowrap;
    position: relative;
    padding: 0.5rem 1.5rem;
    background: rgba(255, 255, 255, 0.03);
    border: 1px solid rgba(255, 255, 255, 0.1);
    clip-path: polygon(8px 0%, 100% 0%, calc(100% - 8px) 100%, 0% 100%);
    transition: all 0.3s;
}

.stack-item::before {
    content: "";
    width: 4px;
    height: 4px;
    border-radius: 50%;
    background: #00f0ff;
    margin-right: 0.8rem;
    box-shadow: 0 0 8px #00f0ff;
    animation: pulse 2s ease-in-out infinite;
}

/* Alternate colors */
.stack-item:nth-child(3n)::before {
    background: #ff2a2a;
    box-shadow: 0 0 8px #ff2a2a;
}

.stack-item:nth-child(5n)::before {
    background: #ffcc00;
    box-shadow: 0 0 8px #ffcc00;
}


.stack-item:hover {
    background: rgba(0, 240, 255, 0.1);
    border-color: #00f0ff;
    color: #00f0ff;
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(0, 240, 255, 0.3);
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

@keyframes shimmer {
    from {
        transform: translateX(-100%);
    }
    to {
        transform: translateX(100%);
    }
}

@keyframes pulse {
    0%, 100% {
        opacity: 1;
        transform: scale(1);
    }
    50% {
        opacity: 0.5;
        transform: scale(0.8);
    }
}


</style>