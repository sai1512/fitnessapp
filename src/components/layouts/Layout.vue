<script setup>

</script>

<template>
    <header>
        <h1 class="text-gradient">Fitness App</h1>
    </header>
    <main>
        <slot />
    </main>
    <footer>
        <p>&copy; 2023 Fitness App. All rights reserved by SAI.</p>
        
        <a href="https://github.com/sai1512" target="_blank">GitHub</a>
    </footer>
</template>

<style scoped>
    header, footer, main {
        padding: 1rem;
        width: 100%;
        max-width: 700px;
        margin: 0 auto;
    }

    main {
        flex: 1;
    }

    footer {
        display: flex;
        flex-direction: column;
        gap: 0.5rem;
        align-items: center;
        padding: 3rem 0;
        padding-bottom: 4rem;

    }

</style>
