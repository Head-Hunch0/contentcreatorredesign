<template>
    <div class="floating-blob"></div>
</template>

<script setup lang="ts">
// No script needed – pure CSS component
</script>

<style scoped>
.floating-blob {
    position: fixed;
    left: 20%;
    top: 70%;
    transform: translate(-50%, -50%);
    width: 500px;
    height: 500px;
    border-radius: 60% 40% 30% 70% / 60% 30% 70% 40%;
    background: linear-gradient(135deg, #ec4899 0%, #f97316 100%);
    filter: blur(60px);
    opacity: 0.4;
    z-index: -1;
    pointer-events: none;
    animation: blobMove 8s ease-in-out infinite, pulseGlow 3s ease-in-out infinite;
}

@keyframes blobMove {
    0% {
        border-radius: 60% 40% 30% 70% / 60% 30% 70% 40%;
        transform: translate(-50%, -50%) scale(1);
    }

    33% {
        border-radius: 30% 60% 70% 40% / 50% 60% 30% 60%;
        transform: translate(-48%, -52%) scale(1.05);
    }

    66% {
        border-radius: 70% 30% 50% 50% / 30% 50% 70% 50%;
        transform: translate(-52%, -48%) scale(0.95);
    }

    100% {
        border-radius: 60% 40% 30% 70% / 60% 30% 70% 40%;
        transform: translate(-50%, -50%) scale(1);
    }
}

@keyframes pulseGlow {
    0% {
        opacity: 0.3;
        filter: blur(60px);
    }

    50% {
        opacity: 0.5;
        filter: blur(70px);
    }

    100% {
        opacity: 0.3;
        filter: blur(60px);
    }
}

/* Responsive: Hide or adjust on smaller screens */
@media (max-width: 1024px) {
    .floating-blob {
        width: 200px;
        height: 200px;
        filter: blur(50px);
        left: 15%;
        top: 75%;
    }
}

@media (max-width: 768px) {
    .floating-blob {
        display: none;
    }
}
</style>