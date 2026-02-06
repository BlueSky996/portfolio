<template>
    <section class="hero">
        <div class="hero-left">
            <h1>Mohamed Khasheebah</h1>
            <p>
                Web3 Full-stack dev
            </p>

            <div class="stack-slider">
            stack slider ( will do later)
            </div>
        </div>

        <div class="hero-right">
            <img src="/images/me.png" alt="Me" />
        </div>
    </section>
</template>

<script>
export default {
    name: "Hero",
};
</script>

<style scoped>
.hero {
    min-height: 100hv;
    display: grid;
    grid-template-columns: 1.2fr 1fr;
    align-item: center;
    padding: 4rem;
    color: white;
}

.hero-left {
    max-width: 600px;
}

.hero-right img {
    width: 100%;
    max-width: 420px;
}
</style>